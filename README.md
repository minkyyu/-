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
  
#### 4.TimeSeriesModeling
* 단변량 시계열 예측
1) 모델 소개
   - ARIMA
   * 출생률 변수만을 이용한 단변량 시계열 모델
   * 자기 회귀, 차분, 이동 평균 항의 차수를 이용한 변수 값 예측
   - Auto ARIMA
   * ARIMA 모델의 최적 하이퍼 파라미터 조합을 자동으로 선택해주는 도구
   * 모델 적합성 판단: AIC가 가장 낮은 모델을 선택
2) 예측 결과

   ![스크린샷 2023-11-12 120956](https://github.com/minkyyu/-/assets/124666194/aca9aed5-2d16-46bd-a6a7-80562ba25c29)

* 다변량 시계열 예측
1) 단변량 예측의 한계
   * 출생률에 영향을 미치는 많은 요인들을 배제하고 출생률만을 가지고 예측하는 것은 예측의 정확성 측면에 부족
   * 출생률의 변동은 다른 외생 변수의 영향도 충분히 있으며, 클러스터별 출생률에 큰 영향을 주는 변수가 다를 수 있다고 판
2) 모델 소개
   * 클러스터별 다중 회귀 분석을 진행하여 다변량 시계열 모델이 활용할 feature를 선택하고, 이에 따른 클러스터별 다변량 시계열 예측 및 분석 진행
   * ADF 검정 및 차분-> 모든 변수에 대한 정상성 확인을 통해 각 변수에 맞는 차분 차수를 할당, 선택된 모든 변수에 대한 차분과 최적의 모델을 결정
   * 해당 클러스터에 가장 적합한 VAR 모델 차수 결정 및 학습
3) 예측 결과

   ![스크린샷 2023-11-12 121841](https://github.com/minkyyu/-/assets/124666194/cee4961f-05ad-4fa5-ae38-4dc07ec36949)

#### 5.Conclusion
* 클러스터별 결과
   * 클러스터1&클러스터3
     - 클러스터1은 모두 아프리카 국가로, 개발도상국으로 이루어져 있고, 클러스터3은 아시아, 중남미의 개발도상국으로 이루어져 있습니다. 그래프로 볼 때 비슷한 수치로 출발했지만 클러스터3이 더 빠른 속도로 출생률이 하락해온 것을 볼 수 있습니다. 
    - 클러스터1은 감소하는 듯 하지만 다시 증가하는 양상을 띄고 있으며, 이는 모델링 전 선택된 변수와 함께 보면 아직 개발이 덜 된 아프리카 지역의 특성이 반영됐고, 이러한 요인들이 빠른 시일 내 변동되지 않을 것이라 볼 수 있다.
    - 클러스터3은 감소하는 양상을 띄고 있으며, 선택된 변수와 함께 보면 클러스터3 또한 여러 생활수준의 지표들의 변동이 크지 않을 것으로 보인다.
   * 클러스터2
     - 선진국과 유럽국가들이 포함되어 있다. 개발도상국에 상관없이 유럽대륙의 특징이 군집의 특성으로 영향을 미칠 것으로 보인다.
     - 클러스터2는 출생률 감소 속도가 매우 낮은 것이 특징으로, 각 국가의 저출산 대응 정책, 문화적 요인 등을 검토하여 다른 군집의 특성으로 영향을 미친 것으로 보인다.
   * 클러스터0 & 한국
     - 한국이 소속되어 있는 클러스터0을 보면 소속 국가들이 선진국보다 개발도상국이 많으며 다른 클러스터에 비해 출생률 감소 속도가 매우 빠른편이다.
     - 클러스터0과 한국을 비교해보면, 유독 우리나라만 출생률이 감소하고 있는 것을 확인할 수 있다. 클러스터0의 선택된 변수가 대부분 경제 성장, 생활 수준과 관련된 지표인데 한국은 클러스터0의 다른 나라에 비해 경제 성장을 단기간에 이룬 선진국에 속한다. 또한 대표적인 국가 발전 지표 중 하나인individuals_using_internet%로 볼 때, 한국의 매우 발전된 인터넷과 스마트폰 사용률이 매우 높은 것이 주요 요인으로 적용했을 것으로 보인다.
* 정책 제안
  * 필수 개선 요소와 벤치마킹을 통해 다음과 같이 정책 제안 가능
   1) 현금 지원 확대와 출산 및 양육으로 얻는 확실한 이득
   2) 출산 및 육아 휴직에 대한 사회 분위기 개선
   3) 교육 정책 개선
   4) 육아 부담 해소
* 한계점 
  * 결측치가 매우 많아 정확한 분석과 예측에 어려움을 겪었다
  * 더 세밀하게 현실 상황을 반영할 만한 변수가 있다면 보다 정확한 분석이 가능했을 것이라 생각합니다
  * Feature의 스케일링의 한계로 변수 선택 과정에 있어 어려움을 겪었다
  * 전공 지식 수준의 한계로 시계열 분석을 진행하지 못했다
  
  
