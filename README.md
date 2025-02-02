# League of legend Match Analysis & Predict to Using Riot API
[![HitCount](http://hits.dwyl.com/tensi3165/League-of-Legends-Match-Predict-Feedback-Project.svg)](http://hits.dwyl.com/tensi3165/League-of-Legends-Match-Predict-Feedback-Project)

> 2019.07.02-2019.09.01 데이터 분석 개인 프로젝트 리메이크

A project to collect league-of-legend game records to analyze the factors that affect victory and to predict winning rates based on real-time score fluctuations.

리그 오브 레전드 경기 기록을 수집하고, 가공하여 승률에 영향을 주는 요인 분석과 스코어 변동에 따른 승률 예측 / 전적 피드백 시스템 구축 프로젝트

![image](https://i.imgur.com/8YdHEAB.jpg)

## 프로젝트 개요

많은 사람이 리그 오브 레전드, 롤을 즐기고 나 또한 이 게임을 매우 좋아하고 즐겨한다. 어릴때부터 친구들과 랭크 경쟁을 하면서 롤을 잘하고 싶었다.

나는 롤을 시즌4, 2014년부터 해온 흔히 말하는 골수 유저인데 티어대가 실버, 골드(상위 30%-40%)에 머물며 매 시즌마다 크게 향상이 없었다. 오브젝트, KDA, 등등 게임 내의 수많은 지표를 보면서 피드백을 해야 승률과 티어가 오르는데 프로도 아니고 개인들이 어디서 객관적인 피드백을 받을 수 있을까.
예를 들어 친구들은 내가 게임의 후반 운영을 할 줄 모른다고 하는데, 정확하게 무엇을 해라 등이 아닌 추상적인 말로 피드백을 한다. 

위의 문제는 나 뿐만이 아니라 게임을 하는 모두가 겪고 자신의 플레이를 객관적으로 분석해주길 바란다. 하지만 프로팀이 아닌 일반인으로서는 객관적인 분석을 받기 어렵다. (프로팀은 코치나, 스태프가 전문적인 분석과 피드백을 지원해준다.)

이를 해결하기 위한 방안으로 자동화 데이터 분석과 머신러닝을 통한 피드백이 있지만, 이를 위해서는 많은 데이터가 필요하다.

현재 E-sports 플랫폼이 크롤링하는 롤 전적 사이트인 OP.GG는 RIOT(롤 개발사)에서 제공하는 API를 이용해 유저의 전적과 게임의 결과를 표시해준다. 이는 Riot-API를 사용하면 경기 전체의 RAW 데이터를 얻을 수 있음을 뜻한다.

따라서, Riot-API를 이용한 개인 프로젝트로 신뢰성 있고 좋은 경기력을 가진 천상계(게임의 최고위 티어인 챌린저, 그랜드마스터, 마스터)의 전적을 수집한다.
이후 데이터 분석과 머신러닝 모델링을 진행해 천상계의 게임은 어떻게 진행되는지, 승률에 미치는 중요한 지표와 해당 지표에 따른 승률을 예측해보고, 전적을 피드백하는 시스템을 개발하여 사람들의 롤 실력 향상에 도움이 되었으면 좋겠다.

## 프로젝트 구성

모든 프로젝트는 Jupyter notebook으로 진행되어 실행결과가 표시되어 있음

또한 ipynb 파일에 세세한 설명과 정리를 해두었으며 데이터만 준비되면 모든 프로젝트가 실행가능함.

### 1. [DATA ETL(Extract, Transform, Load)](https://github.com/tensi3165/League-of-Legends-Match-Analysis-and-Predict/blob/master/1.Match%20Data%20ETL.ipynb)

> 2019.07.02 - 2019.08.23

RIOT에서 제공하는 API를 이용해 데이터를 수집하고 가공하고, 파일화하여 저장한다.

* 결과 : 챌린저, 그랜드마스터, 마스터 티어의 약 180000개 롤 경기데이터 수집, 캐글 데이터셋에 공개되어있음.

* 한계 : Riot api 중 timeline api로 각 경기의 시간대별 이벤트 로그를 수집할 수 있었지만, 컴퓨팅 자원의 문제로 수집하지 못했고, 굉장히 전처리가 어려운 구조였다.

### 2. [Match Data EDA(Exploratory Data Analysis)](https://github.com/tensi3165/League-of-Legends-Match-Analysis-and-Predict/blob/master/2.Data%20EDA.ipynb)

> 2019.08.24 - 2019.08.25

모은 데이터를 분석에 용이하도록 전처리하고, 승패에 영향이 가는 변수를 분석한다.

* 결과 : 패치버전 외부데이터 크롤링으로 해당 경기기록은 2020 - 2018 년의 경기기록이란 것을 앎, 승리에 중요한 지표를 알아냄, 경기 시간대별로 승리에 중요한 지표가 다름을 발견함.

* 한계 : 시계열 데이터를 통한 시간대별 분석이었으면 더 흥미로운 통찰 결과가 나왔을 것 같다.

### 3. [Feature Engineering & Modeling](https://github.com/tensi3165/League-of-Legends-Match-Analysis-and-Predict/blob/master/3.Analysis%20Modeling.ipynb)

> 2019.08.26 - 2019.09.01

EDA를 통해 얻은 정보로 특성 공학을 진행하고,

승패 예측을 진행할 모델을 구축한 뒤 튜닝을 통해 예측의 정확도를 올려 신뢰성 있는 모델을 만든다.

회귀 분석과 특성 중요도 시각화로 모델을 분석하고, 해당 지표가 얼마나 승률에 영향을 미치는가 확인.

* 결과 : 팀의 분당 성장률을 나타내는 지표 생성으로 시간당 특성 가중치가 다름을 표현함, 단순한 총합값이 아닌 비율값으로 변환, 다중공선성 제거, 
경기 이후 데이터를 경기 진행중일때의 지표로 변환하고 독립변수 간의 상관관계를 제거하는 것이 중요한 포인트였음. 

LogisticRegression, Random Forest, XGBoost, Catboost 모델을 사용하여 정확도 97.9-98.0% 에 달하는 모델 완성

* 한계 : 수집한 데이터셋은 경기가 끝나고 난 후의 데이터로 승패 예측에 굉장히 과적합되기 쉬워 그걸 완전히 제어하지 못했고, 약간의 과적합이 발생했다.

### 4.[Project Analytics & Result](https://github.com/tensi3165/League-of-Legends-Match-Analysis-and-Predict/blob/master/4.Collect%20UserData%20Pipeline.ipynb)

> 2019.09.03 - 2019.11.12( 랭크 게임 종료시까지 )

실제 자신의 전적을 불러와 테스트를 진행하고, 피드백 알고리즘 구성.
프로젝트 마무리와 해당 피드백을 중심으로 게임을 하고 달성한 티어대 기록.

* 결과 : 실시간으로 자신의 롤 닉네임을 이용해 전적을 조회할 수 있도록 하고, 특성 공학에서 찾아냈던 지표로 변환하여 보여준 뒤, 자신이 팀에서 얼마나 기여했는지를 표시, 자신의 최근 전적 1-20개까지 분석할 수 있도록함. 

이 함수를 통해 얻은 데이터는 훈련/테스트 데이터의 형태와 일치하므로,분석 데이터를 훈련셋에 포함하면 실시간 온라인 학습 또한 가능함.

해당 데이터 분석과 피드백을 통해 승률이 11% 높아짐.(승률 43% → 54%) 또한 본인과 친구의 롤 랭크 플레티넘 → 다이아 달성.(상위 10% → 2%)

* 한계 : Riot API는 초당 20개, 분당 50개의 요청 제한이 있는데 이에 따라 분석할 수 있는 경기가 강제로 1개부터 20개까지로 제한되며, 동시에 3명 이상의 분석은 거의 불가능함.(단, 1명당 1개의 분석을 요청할 경우 20명까지 분석할 수 있음.)

추가적으로 편하게 해당 시스템을 이용할 수 있도록 Kakao Chat BOT 형태로 개발중.

## 업데이트 내역

* (2020.03.20)
  
  DATA ETL 데이터 업데이트

* (2020.04.28)

  Repository 재생성, 정리

* (2020.05.18)

  Code clean up, Refactoring
  
## ALL DATA SET LINK

모든 데이터 셋은 Kaggle 에 공개하였음.

<https://www.kaggle.com/shinbg/lol-classic-rank-game-datakrtop-3-tier>

코드 복제와 데이터 셋 사용은 자유이며 다른 사람도 유용한 인사이트를 도출해 실버 골드를 탈출하길 바람.
