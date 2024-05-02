# NLP_test

## Задача бинарной классификации (спам/не спам) сообщений на английском языке.

### EDA


Для начала посмотрим на примеры сообщейний разных классов:


 Example | Class |  
:------------:|:------------:|
 do i require an attorney to use this system and clean up my record purge all of your card payments cancel debts and never make another payment discharge debts quickly painlessly legally for the rest of the story about canceling debt go to our elimination pages no then the link and address above king edward was engaged in earnest consultation with one of his ministers and after a look of surprise in rob s direction and a grave bow he bestowed no further attention upon the intruder but rob was not to be baffled now your majesty he interrupted i ve important news for you | spam 
any lady around lucky summer inbox for hookup | spam  
mera naam hai priya mujhe party me jana dance karna acha lagta hai kya aap mujhse dosti karoge? dial 5512111 rs2/min | spam 
last year some frankfinnians started with a salary of rs 1 26 lacs pm this year it could be u for details sms ffn to 5616111  | spam 
post jobs fast and get results fast 100 s of employers are posting jobs here make your next career move and log on to jobslog com make a free resume and find lots of free career tips at our resource center jobslog com 1314 south king st ste 856 honolulu hawaii 96814 this e mail message is an advertisement and or solicitation | spam
here s a 4 th try rick i shall ask my assistant to schedule a meeting early next week vince richard b jones ees 02 01 2001 10 23 am to vince j kaminski hou ect ect cc subject here s a 4 th try forwarded by richard b jones hou ees on 02 01 2001 10 22 am richard b jones 01 31 2001 04 39 pm to vince j kaminski hou ect ect cc subject here s a third try vince while i was at hsb i designed an insurance or reinsurance financial model that hsb uses for new product development pricing different reinsurance strategies computing stochastic earnings forecast and estimating probabilistic maintenance repair costs the code written in visual basic ms access belongs to hsb and i want to rep | ham
which cmd? | ham
sorry about earlier putting out firesare you around to talk after 9 or do you actually have a life lol | ham
saiman youtuber? | ham
both looks good | ham


На распределении по классам видно, что соотношение 2 к 1 в в пользу `ham`

![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/f4318afa-0079-423f-a72a-7f971f812df0)

Исходя из примеров выше, можно предположить что обычные сообщения в среднем более короткие, чем `spam` проверим, так ли это

Распределение длин сообщений в словах          |  Распределение длин сообщений в  символах
:-------------------------:|:-------------------------:
<img src="https://github.com/BerezinDaniil/NLP_test/assets/78606208/57826127-7746-40df-96c3-4021443b3382" width="555" /> | <img src="https://github.com/BerezinDaniil/NLP_test/assets/78606208/1774fb61-aa72-48ad-b756-00ebc6930452" width="500" />

Видим, что данная теория имеет место быть.

### Models

## Logistic Regression + EDA features
Первую модель логистической регресии попробуем построить на 3х фичаx:

 * Длина сообщения в словах

 * Длина сообщения в символах

 * Наличие в сообщении `$` (флаг того, что сообщение про доход и прочее )

Результат получился лучше случайного, однако это мало )))


![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/6342211d-21cf-4385-955e-be9292c2018d)


## Tf-idf + LogisticRegression and Naive Bayes
Попробуем "классику" классификации спама - Naive Bayes

Для векторизации сразу будем использовать `tf-idf`, перед этим преобразуем текст: 

 * Удаление стоп слов

 * Удаление стикеров и специальных символов

 * Стемминг

Посмотрим на двумерное представление `tf-idf` полученное с помощью `SVD`

![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/09da8ff7-262a-423b-a163-8e28a889b40f)

Видим, что данные визуально неплохо разделимы, что придает оптимизма) 

### Naive Bayes

`Accuracy`   |  `F1` |  `AUC`
:----:|:-----:|:-----:
0.814 | 0.709 | 0.904|

![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/1d1520e2-44ed-41e4-a392-a6d1b32ccb49)

### LogisticRegression

`Accuracy`   |  `F1` |  `AUC`
:----:|:-----:|:-----:
0.90 | 0.87 | 0.965 |

![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/a41a8118-ec03-483b-9527-f7254e94b9d9)

#### Shap

Посмотрим на важность фич для  `LogisticRegression` с помощью библиотеки `Shap`

![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/2cc4553e-3d32-46d8-833b-5f90d603a3bd)

Видим множество фичей, пересекающихся с нашей гипотизой, про связь  рекламы "зароботка" и "бизнеса" - `offer`, `free`, `earn`
А так же слова призывающие куда-то нажать - `link`,`account`, `click`, `call`

### LogisticRegression + feature selection
TO DO
Попробуем отобраить некий топ важных для классификации слов и построить модель только на них


## CatBoost

Посмотрим, как справится с векторизацией встроенные методв `CatBoost`

`Accuracy`   |  `F1` |  `AUC`
:----:|:-----:|:-----:
0.962 | 0.952 | 0.989 |

![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/c83a5169-2526-4263-b5a5-528083005507)

Получаем отличный результат - 0.989 `AUC`, кажется можно остановится, но можно ли лучше? 


## BERT
Для классификации будем использовать предобученную модель `distilbert` (более легковестный `BERT`)

`Accuracy`   |  `F1` |  `AUC`
:----:|:-----:|:-----:
0.964 | 0.956 | 0.992 |


![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/d1fe488c-53b3-4e9e-b237-b81b751b1d2b)

Получаем почти идиальный результат 

### Shap





