# mge51101-20196032

```
Name : Jinsu Jeon
Student No. : 20196032
School : Business Analytics
E-mail : yg99192@unist.ac.kr
```

# final project


## 1. introduction
Text data is piled up extensively over the Internet. In the past, public opinion gathering was mostly possible by voting or by telephone. However, the development of IT technology makes the Internet accessible to most people, creating public opinion through the Internet. This study seeks to collect policy-related Internet news as COVID-19 spreads to see how public opinion forms on the Internet.
People express their opinions a lot on NAVER, Korea's largest portal site. In particular, it is necessary to check the formation of public opinion on policy news. It puts a label on the comment and creates a deep learning model to classify the opinion of the comment that is constantly being expanded and reproduced. Through this, check whether comments related to policy are negative or positive on the Internet.

## 2. Data Description
Comments were crawled from March 1 to May 31 to collect news related to government policy and COVID-19 spread. The title of the news article excludes articles that are too political or have nothing to do with government policy. For example, if they had news articles with keywords far from government policy, such as ballet, Lee Man-hee, and Samsung, they were excluded. Finally, 505,743 comments were collected. KOMORAN which is Korean preprocessing library is used. Due to the nature of Internet comments, Internet terms should be added as nouns. For example, the keyword 'Moon Jae-ang' is an important word, but it is not collected as a noun. KOMORAN was used because it was relatively fast and easy to add new nouns. Even using a noun extractor, words that are not nouns are sometimes extracted. In this case, min_count was given to extract the word used at least three times. Also, we extracted a word that is more than 2 length, and finally, we specified stopwords to extract only meaningful nouns as much as possible. Input is the noun of each comment and output is the label value divided into anti-government cognition. Labels calculated from output were labelled using methods, and 405,330 of the total 505,743 comments were labelled as anti-government comments. The rate is about 80 percent.

|댓글|명사추출된 댓글|Judgement|
|---|---|---|
|정부보다 낫네요! 감사합니다.|['정부', '감사']|Good|
|국민들은 죽어가는데 퍼주기대장...도움은못되도 피해는주지말아야지요~|['국민', '대장', '도움', '피해']|Bad|
|여러분 속지마세요. 대깨문중 49%라는 소리임|['여러분', '대깨문', '소리']|Bad|
|매번 고개숙이고 겸손한 대통령님..항상 응원합니다|['고개', '겸손', '대통령님', '응원']|Good|

## 3.Method
#### 3-1 wor2vec
Labeling is important to classify out Internet comments whether it is anti-government or not. Get Word2vec Embedding matrix of 505,743 comments. 35698 nouns were extracted. After that, find Euclidean distance between words and map it in a high dimension through the Rbf kernel. This results in the (35698, 35698) inter-word distance matrix. It then designates the anti-government pro-government Keyword based on prior knowledge. A total of 53 keywords were used, consisting of 36 anti-government words and 17 pro-government words. TDM is extracted from the comments and dot product them with this matrix. The similarity between each comment and keyword is calculated. The average of the top five distances of the antigovernment keyword and the top five distances of the pro-government keyword are obtained. When the anti-government is bigger, the comments specify the label as anti-government comments. The opposite all sets out label in pro-government word.
#### 3-2 Deep-learning Algorithms
Use word2vec embedded matrix as input value. Use mode of comments to match length. The mode of comment length was 30. We used CNN algorithms that configured channels 3,4,5 and LSTM and GRU, which are frequently used in text data. CNN referred to Yoonkim's textclassification. Each CNN1D layer passed through the kernel size of [3,4,5] and concatenate after apply maxpooling. Then, passed through the concatenated layer as kernel size 3. Flat the Layer and then make is as fully-connected layers. Finally, let's have a binary classification of 0,1 by sigmoid function. when I used LSTM and GRU, I didn't build layers deep. Model evaluation has set up accuracy and AUC. Accuracy is the most intuitive value. AUC is also frequently used when data forms are imbalanced. In other words, it was necessary to find out if the anti-government accounts were actually well classified.

## 4. Experiment
#### 4-1 result
|Model|Train Acuuracy(AUC)|Val Accuracy(AUC|Test Accuracy(AUC)|
|---|---|---|---|
|CNN|0.971(0.994)|0.963(0.990)|0.963(0.989)|
|LSTM|0.947(0.963)|0.959(0.989)|0.960(0.989)|
|GRU|0.945(0.981)|0.956(0.988)|0.957(0.988)|

The test was conducted using three models, CNN, LSTM, and GRU. All three had no vanishing gradient problems and were well learned without overfitting. Accuracy and AUC were high in all models. Maybe it is because it is consistently labelled based on Word2vec.
#### 4-2 loss curve


![image](https://user-images.githubusercontent.com/62274298/85069324-e32e0c00-b1ee-11ea-9ac6-eff1af1fe621.png)
Because of binary classification, I gave binary_cossentropy as lossfunction. ADAM was used to optimize and gave the default value. Train/test was randomly classified based on the proportion of the target variable. The batch size was allocated as 100. Epoch allocated 30 but as soon as the model learned several times, it recorded high accuracy and was learned within 10 times by early stopping.

## 5.Conclusion
A large amount of text data was labelled and classified into deep learning algorithms like CNN,LSTM,GRU. It was learned with about 500,000 text data and its classifier performance was also good. However, we need to verify that the labelling is accurate. Also, there will be a neutral comment in the current binary classification.I think deep learning performance will also change if class is subdivided into five classes like very anti-government, a little anti-government,neutral, a little pro-government, and a very pro-government. In addition, through this project, I experienced the strength of deep learning in unstructured data and identified the importance of embeddeding matrix in NLP. I hope to develop this project later to create a taxonomy that can check the public opinion of comments and contribute to the establishment of government policies. 






