# mge51101-20196032

```
Name : Jinsu Jeon
Student No. : 20196032
School : Business Analytics
E-mail : yg99192@unist.ac.kr
```

### final project(Temp)

1.네이버 뉴스댓글분류를 통한 여론형성 확인

뉴스댓글 조작에 관한 이슈들이 있었습니다. 김경수 도지사의 드루킹 , 문재인 차이나게이트 등 네이버 뉴스댓글을 통해 여론이 좌지우지 되는것 같아보였습니다.

그래서 저는 네이버댓글들을 분류하여 여론이 어떻게 퍼져지는지 분석해보고 싶습니다. 댓글들을 보면 major한 댓글과 minor한 댓글로 나눌수 있다고 치면
베스트댓글이 나머지 댓글들에 어떻게 영향을 미치는지 검증하고 싶습니다.

<img width="496" alt="네이버뉴스댓글" src="https://user-images.githubusercontent.com/62274298/77391383-f3933e00-6ddb-11ea-92d4-2e33a211d22d.png">




그러기 위해선 댓글을 분류할수 있어야합니다. 예를들어 코로나 사태가 터졌을 때 댓글들이 친정부/반정부/중립 으로 나누어서 베스트 댓글들이 반 정부적인 댓글이 많을 때 친정부적인 댓글들의 분포를 알아야합니다.

CNN / LSTM / ELMo / BERT 등 다양한 딥러닝 알고리즘을 적용하여 문장을 분류해 내는것이 목표입니다.




2. 제조데이터(시계열)를 이용한 defect detect

제조업에서 time series 분석을 통해 양품인지 불량품인지 파악하고 불량이라면 무슨 불량인지 분석을 하고싶습니다.

![good_data](https://user-images.githubusercontent.com/62274298/77392334-04dd4a00-6dde-11ea-97b1-7441f96e9989.png)

<양품>


![bad_data](https://user-images.githubusercontent.com/62274298/77392350-0dce1b80-6dde-11ea-9fd1-ea1c5142e437.png)

<불량품>



COTE / 뉴럴넷 앙상블 / MCNN / LSTM-FCN 등 시계열 분류에 사용되는 알고리즘으로 공정데이터들의 불량파악을 95%이상 분류해 내는것이 목표입니다.



3. 문장 생성을 통한 자동보고서 작성

인터넷에 있는 뉴스기사/ 그래프 / 그림을 input으로 넣어 보고서를 작성해주는 프로젝트를 해보고싶습니다.

LSTM이나 트랜스포머 구조를 정확히 이해하고 , input을 넣었을때 자동으로 문장을 생성해주는 프로젝트를 진행해보고 싶습니다.
