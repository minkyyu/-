# -건국대학교 응용통계학과 제4회 통계최강자전

## 수상 결과: 
## 대회 기간: 23.09.10 ~ 23.10.15
## 대회 데이터셋
-Fifa World Cup 2022

-Bike Sharing

-World Bank World Development Indicators

-Heath Checkup Result

-Passenger Satisfaction

-선정한 데이터셋 출처:<https://www.kaggle.com/datasets/nicolasgonzalezmunoz/world-bank-world-development-indicators>

------

## 주제: 국가 개발 지표를 통한 출생률 예측 및 통계 분석

#### 1.Introduction
* 주제 선정 배경
1) 한국 저출산 문제의 심각성
   OECD 국가 중 가장 출생률이 낮아지고 있다.

   -> 인구 소멸 위기에 직면
   문제 해결을 위해 출생률 예측과 미래 인구 구조 파악이 중요하다.

   -> 출생률의 심각성을 인지하고 지속 가능한 발전을 위한 여러 방안 모색 가능
3) 저출산 정책 개선
   OECD 국가를 포함한 다양한 국가의 출생률과 사회경제적 특성 비교 분석
   타 국가의 사례와 상황 분석을 통한 인사이트를 얻고, 벤치마킹을 통한 전략적 정책 개선이 필요하다.
* 분석 목표
1) 출생률에 영향을 미치는 요인 파악
2) 출생률 추이에 따른 클러스터링
3) 출생률 예측 모형 개발 및 예측
#### 2.Data Exploration
* 선정 데이터 탐색
1) 데이터의 설명 변수를 출생률 예측에 맞는 여러 요인으로 분류
2) 출생률과의 상관성을 고려한 외부 데이터 결합
* 전처리
1) 변수 변환
   Count로 된 값 이루어진 변수들을 인구수로 나눠 1인당 지표로 변환

   ex)GDP, GNI, 영아 사망자 수
3) 변수 삭제
   결측치가 70% 이상인 변수 삭제

   출생률과 매우 동떨어진 변수 삭제

   출생률과 상관관계 및 다중공선성 의심 변수 삭제
4) 결측치 대체
   선형 보간법을 통한 결측치 대체

   ->시계열 데이터 특성 고려
* EDA
  기술통계량 확인을 통한 데이터 특성 파악

  Target 변수 분포 확인

  각 요인별 Feature 변수 분포 확인
* Features Scaling
  EDA를 통해 변수들에 많은 이상치 파악 및 데이터 분포 비정규성 확인

  -> target 변수를 제외한 feature 변수에 'MinMaxScaling' 방법 적용
  
#### 3.TimeSeries Clustering
* 출생률 클러스터링
  국가마다 출생률 수치와 추이가 다른 것을 확인 -> 비슷한 국가별로 군집화하는 것이 보다 정확한 모델 학습과 예측으로 이어질 것으로 판단
* 군집 갯수 선정 방법
  Elbow Method, Silhouette Score를 활용하여 판단 결과, 4개의 군집으로 구분
* 클러스터별 Birth_rate 추세 확인
  각 클러스터에 속한 국가별 출생률 비교 결과, 대체적으로 확실하게 군집이 잘 나뉘어진 것으로 확인
  ![스크린샷 2023-11-12 115223](https://github.com/minkyyu/-/assets/124666194/54363782-7e45-4793-96a8-575414f0c52c)
  
#### 4.Univariate TimeSeriesModeling

#### 5.Mulivariate TimeSeriesModeling

#### 6.Conclusion



