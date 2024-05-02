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

Исходя из примеров выше, можн опредположить что обычные сообщения в среднем более короткие, чем `spam` проверим, так ли это


![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/57826127-7746-40df-96c3-4021443b3382) ![image](https://github.com/BerezinDaniil/NLP_test/assets/78606208/1774fb61-aa72-48ad-b756-00ebc6930452)



