# mge51101-20196032

```
Name : Jinsu Jeon
Student No. : 20196032
School : Business Analytics
E-mail : yg99192@unist.ac.kr
```

# final project(Temp)


## 2. Data Description

#### 2-1 수집방법

네이버에 코로나 19를 치면 다음과 같이 많은 뉴스들이 검색됩니다
<img width="1080" alt="1" src="https://user-images.githubusercontent.com/62274298/78859716-2475a300-7a6b-11ea-9cdd-2c40bc6c63e5.png">


이 때 다음의 네모친 링크로 접속을 하게 되면 뉴스기사로 링크로 접속이 되는데 다음과 같은 댓글을 확인할수 있습니다.
<img width="519" alt="뉴스검색창" src="https://user-images.githubusercontent.com/62274298/78859767-50912400-7a6b-11ea-96b7-df71284d0097.png">


여기서 댓글, 좋아요, 싫어요, 날짜 를 수집하게 되면 다음과 같은 자료구조를 형성하게 됩니다.

|댓글|날짜|좋아요|싫어요|
|---|---|---|---|
|2020-03-06T22:43:56+0900|ㅊㅊㅊㅊ문재인의 일본에 대한 보복조치가 설득력을 얻기 위해서는, 중국의 한국인 입국 제한조치에 대해서도 상응조치를 해야 한다 왜 문재인은 중국에 대해서는 상응조치는 커녕, 항의 한마디 못하나? 중국이 상전인가?   일본이라면 무조건 '죽창으로 왜놈 때려 잡겠다'고 흥분하는 무식하고 개념없는 인간들  또 반일 감정 자극해서, 부추키고 동원 하려고 하나?|0|0|
|2020-03-04T21:59:44+0900|대구경북 1당독재피해  수도권 중국인 왕래가 제일 많아   사망자 제로 이재명 박원순 델코온나    경북사람아닌가?|0|0|
|2020-03-03T13:56:54+0900|매번 고개숙이고 겸손한 대통령님..항상 응원합니다|1|30|
|2020-03-06T20:40:37+0900|웃기고 있다~ 짱개한테는 암말 못하면서 오직 일본한테만 초강경 대응이란다 ㅋㅋㅋㅋㅋ 우리도 총선때 니들한테 초강경대응 할란다^^|263|18|


1. introduction
Text data is piled up extensively over the Internet. In the past, public opinion gathering was mostly possible by voting or by telephone. However, the development of IT technology makes the Internet accessible to most people, creating public opinion through the Internet. This study seeks to collect policy-related Internet news as Corona 19 spreads to see how public opinion forms on the Internet.
People express their opinions a lot on NAVER, Korea's largest portal site. In particular, it is necessary to check the formation of public opinion on policy news. It puts a label on the comment and creates a deep learning model to classify the opinion of the comment that is constantly being expanded and reproduced. Through this, check whether comments related to policy are negative or positive on the Internet.

2. Data Description
Comments were crawled from March 1 to May 31 to collect news related to government policy and COVID-19 spread. The title of the news article excludes articles that are too political or have nothing to do with government policy. For example, if they had news articles with keywords far from government policy, such as ballet, Lee Man-hee, and Samsung, they were excluded. Finally, 505,743 comments were collected. KOMORAN which is Korean preprocessing library is used. Due to the nature of Internet comments, Internet terms should be added as nouns. For example, the keyword 'Moon Jae-ang' is an important word, but it is not collected as a noun. KOMORAN was used because it was relatively fast and easy to add new nouns. Even using a noun extractor, words that are not nouns are sometimes extracted. In this case, min_count was given to extract the word used at least three times. Also, we extracted a word that is more than 2 length, and finally, we specified stopwords to extract only meaningful nouns as much as possible. Input is the noun of each comment and output is the label value divided into anti-government cognition. Labels calculated from output were labelled using methods, and 405,330 of the total 505,743 comments were labelled as anti-government comments. The rate is about 80 percent.
3.Method
3-1 wor2vec
Labeling is important to classify out Internet comments whether it is anti-government or not. Get Word2vec Embedding matrix of 505,743 comments. 35698 nouns were extracted. After that, find Euclidean distance between words and map it in a high dimension through the Rbf kernel. This results in the (35698, 35698) inter-word distance matrix. It then designates the anti-government pro-government Keyword based on prior knowledge. A total of 53 keywords were used, consisting of 36 anti-government words and 17 pro-government words. TDM is extracted from the comments and dot product them with this matrix. The similarity between each comment and keyword is calculated. The average of the top five distances of the antigovernment keyword and the top five distances of the pro-government keyword are obtained. When the anti-government is bigger, the comments specify the label as anti-government comments. The opposite all sets out label in pro-government word.
3-2 Deep-learning Algorithms
Use word2vec embedded matrix as input value. Use mode of comments to match length. The mode of comment length was 30. We used CNN algorithms that configured channels 3,4,5 and LSTM and GRU, which are frequently used in text data. CNN referred to Yoonkim's textclassification. Each CNN1D layer passed through the kernel size of [3,4,5] and concatenate after apply maxpooling. Then, passed through the concatenated layer as kernel size 3. Flat the Layer and then make is as fully-connected layers. Finally, let's have a binary classification of 0,1 by sigmoid function. when I used LSTM and GRU, I didn't build layers deep. Model evaluation has set up accuracy and AUC. Accuracy is the most intuitive value. AUC is also frequently used when data forms are imbalanced. In other words, it was necessary to find out if the anti-government accounts were actually well classified.

4. Experiment
4-1 result
The test was conducted using three models, CNN, LSTM, and GRU. All three had no vanishing gradient problems and were well learned without overfitting. Accuracy and AUC were high in all models. Maybe it is because it is consistently labelled based on Word2vec.
4-2 loss curve
Because of binary classification, I gave binary_cossentropy as lossfunction. ADAM was used to optimize and gave the default value. Train/test was randomly classified based on the proportion of the target variable. The batch size was allocated as 100. Epoch allocated 30 but as soon as the model learned several times, it recorded high accuracy and was learned within 10 times by early stopping.

5.Conclusion
I labelled the Internet comments to sort out whether they were anti-government or not based on deep learning. I think it will help us assess whether the Label is appropriate and if it goes well, it will help us understand the public opinion of the comments.








