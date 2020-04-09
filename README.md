# mge51101-20196032

```
Name : Jinsu Jeon
Student No. : 20196032
School : Business Analytics
E-mail : yg99192@unist.ac.kr
```

# final project(Temp)

### 1. Goal 침묵의 나선효과 이론을 텍스트마이닝으로 검정

침묵의 나선효과란
기본적으로 인간은 고립되거나 배척되는 것에 대한 두려움을 갖고 있고, 다수에게 받아 들여지기를 원한다. 때문에, 특정한 문제가 발생했을 때 이에 대한 여론을 면밀히 관찰하고, 자신의 의견과 다수가 지지하는 지배적인 여론이 일치한다는 확신이 생길 경우, 자신의 의견을 공공연히 표방하게 된다. 반대로 자신의 의견과 다수의 의견이 상충되거나, 자신의 의견이 소수 쪽에 속할 경우에는 침묵하는 경향이 있다. 때문에 주류에 속하게 된 의견은 확대 포장될 가능성이 생기고, 소수 의견은 과소평가되는 결과가 나올 수 있다. -by 위키피디아-

이 이론이 실제 익명의 공간인 인터넷상에서도 적용되어 지는지 확인하겠습니다. 다수의 의견이 굉장히 친정부적 성향인데 반정부적 성향의 댓글이 얼마나 존재하는지, 혹은 그 반대일 땐 어떤지 , 가장 큰 뉴스포탈인 네이버에서 확인해보고 싶습니다.


## 2. Data Description

#### 2-1 수집방법

네이버에 코로나 19를 치면 다음과 같이 많은 뉴스들이 검색됩니다
<img width="1080" alt="1" src="https://user-images.githubusercontent.com/62274298/78859716-2475a300-7a6b-11ea-9cdd-2c40bc6c63e5.png">


이 때 다음의 네모친 링크로 접속을 하게 되면 뉴스기사로 링크로 접속이 되는데 다음과 같은 댓글을 확인할수 있습니다.
<그림2>




여기서 댓글, 좋아요, 싫어요, 날짜 를 수집하게 되면 다음과 같은 자료구조를 형성하게 됩니다.

|댓글|날짜|좋아요|싫어요|
|---|---|---|---|
|2020-03-06T22:43:56+0900|ㅊㅊㅊㅊ문재인의 일본에 대한 보복조치가 설득력을 얻기 위해서는, 중국의 한국인 입국 제한조치에 대해서도 상응조치를 해야 한다 왜 문재인은 중국에 대해서는 상응조치는 커녕, 항의 한마디 못하나? 중국이 상전인가?   일본이라면 무조건 '죽창으로 왜놈 때려 잡겠다'고 흥분하는 무식하고 개념없는 인간들  또 반일 감정 자극해서, 부추키고 동원 하려고 하나?|0|0|
|2020-03-04T21:59:44+0900|대구경북 1당독재피해  수도권 중국인 왕래가 제일 많아   사망자 제로 이재명 박원순 델코온나    경북사람아닌가?|0|0|
|2020-03-03T13:56:54+0900|매번 고개숙이고 겸손한 대통령님..항상 응원합니다|1|30|
|2020-03-06T20:40:37+0900|웃기고 있다~ 짱개한테는 암말 못하면서 오직 일본한테만 초강경 대응이란다 ㅋㅋㅋㅋㅋ 우리도 총선때 니들한테 초강경대응 할란다^^|263|18|

#### 2-2 Data Preprocessing

##### a. storpwords
'괜히','또또','사방','려면','다해','왜또','부터'
다음과 같은 의미없는 단어들을 제거 후 분석하겠습니다. 


##### b. Twitter 명사추출기

이 방법을 쓴 이유는 인터넷상으론 줄임말이 굉장히 많습니다.
예를들어 질병본부를 질본 이라던지 , 그런 줄임말들을 dictionary에 추가를하면 명사로 인식해줘서 분석을 진행해주기 때문에 선정했습니다.


## 3 . Model 

다양한 임베딩을 한 후  CNN 과 RNN을 사용하여 분석해 보겠습니다. 차후에 가능하면 ELMO와 같은 다양한 임베딩을 적용하여 문장분류를 해보겠습니다.

## 4. Model evaluation

AUC Score
Accuracy Score
F1 score

데이콘에서 nlp분류를 했을 때도 AUC score를 비교하였습니다. 주로 AUC를 쓰되 추가로 정확도와 F1-scroe를 통해 비교해보겠습니다.
## 5. Diffuculty

##### 5-1 . Labeling

데이터에 기본적으로 Labeling이 되어있지않습니다. 저는 이 방법을 Word2vec과 TDM matrix를 곱하여 단어와 댓글관의 연관성을보고 threshhold값을 지정해서 score에 따라 댓글이 반정부/친정부/중립인지 분류하겠습니다. 라벨링이 제대로 되었는지 안되었는지는 후에 제가 labeling을 2000개 정도 해보고 비교해보겠습니다.

이와같이 labeling을 하면 댓글에서 완전히 새로운 명사가 들어오면 word2vec에서 분류를 못합니다. 그래서 코로나 19로 수집된 20만개가량 댓글이 있는데
하나의 큰 matrix를 구해서 완전히 학습될수있도록 하겠습니다.
##### 5-2 preprocessing

명사만 추출해서 라벨링을 하면 한계가 있을 것같습니다. 
##### 5-3 







