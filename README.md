# <a href="https://aifactory.space/task/2511/overview" target="_blank">2023 제1회 철도 인공지능 경진대회</a>
## 🚩 대회 정보
- 주제 : 열차의 주행 안정성 진단에 사용되는 ‘탈선계수’를 보다 높은 정확도로 예측할 수 있는 인공지능 모델 개발
- 기간 : 23.08.01 ~ 23.09.21
- 팀명 : 한국철도999 (총 4명)
- 결과 : 5위 / 68팀 (78.681525점)
- 수상 : 장려상🥉
<br>

## ✔대회 설명
- 주어진 주행데이터 및 선로데이터를 이용하여, **탈선계수**에 해당하는 이하 4개 항목을 예측하는 모델을 만듭니다.
    - YL_M1_B1_W1: 좌측 전위 차륜 탈선계수
    - YR_M1_B1_W1: 우측 전위 차륜 탈선계수
    - YL_M1_B1_W2: 좌측 후위 차륜 탈선계수
    - YR_M1_B1_W2: 우측 후위 차륜 탈선계수
      
- **직선구간(data_s)** 데이터와 **곡선구간(data_c)** 데이터가 yaw damper의 비선형제어능력 조건에 따라 각 5개씩 주어집니다.
    - 총 10개 데이터 파일마다 탈선계수 4열씩, 총 40열의 데이터를 예측합니다.
    - 실제 데이터는 3km 길이 만큼 주어지며, 예측 대상은 마지막 500m에 해당되는 구간입니다.
      
- 모델은 **반드시 다음의 조건을 충족**해야 합니다.
    - **각 탈선계수의 과거 시점 값 또는 각 탈선계수의 자기상관 데이터를 독립변인으로 사용하는** **시계열/패널 유형** **모델**일 것
        - 탈선계수의 과거 시점 값(t-1 … t-M)과 그 외 변인들(예: 구간 정보)의 대상 시점 값(t … t+N)을 함께 활용하여 예측 수행
        - 예측 시 사용할 과거 시점 값의 길이와 한 번 예측에서 생성할 예측 시점의 길이는 자유
        - 한 번에 전체 대상 시점에 대한 예측 생성이 어려운 경우, 생성한 예측을 다시 입력으로 활용하여 다음 시점을 생성하는 모델을 구축
          
    - **전체 단일 모델** 또는 **직선구간 모델**과 **곡선구간 모델**의 형태로 모델을 생성할 것
        - 직선구간과 곡선구간 데이터의 선로 정보 구성 항목이 서로 다른 점에 유의
        - 앙상블에 대한 제약은 없으나, **2차 평가항목에 활용성이 포함**되어있음에 유의
          
## 📑 데이터
```
📁 dataset.zip
 ├--- 📁 data_c                     --- 곡선(curve) 선로 주행 데이터
 ├--- 📁 data_s                     --- 직선(straight) 선로 주행 데이터
 ├--- 📁 data_columns               --- 선로 주행 데이터 컬럼 설명
 ├--- 📁 lane_data                  --- 선로 센서 데이터
 ├--- 📁 lane_data_columns          --- 선로 센서 데이터 컬럼 설명
 └--- 📃 answer_sample.csv          --- 정답 양식 파일
 ```
- data_c: 곡선 선로를 주행할 때 기차의 센서 데이터입니다. 'yaw damper'에 따라 30, 40, 50, 70, 100, 5개의 데이터로 구성됩니다.
- data_s: 직선 선로를 주행할 때 기차의 센서 데이터입니다. 'yaw damper'에 따라 30, 40, 50, 70, 100, 5개의 데이터로 구성됩니다.
- data_columns: data_c, data_s의 컬럼에 대한 설명 데이터입니다.
- lane_data: 주행한 선로의 데이터입니다. 직선 선로, 곡선 선로로 나뉘어 있습니다.
- lane_data_columns: 선로 데이터 칼럼에 대한 설명 데이터입니다.
- answer_sample: 각 데이터의 탈선 계수 예측값을 입력하는 양식입니다.
<br>

## 📈 AI 모델링
#### 1. 사용 모델
<p align="center"><img src="https://github.com/ayocado/2023_Railroad_Contest/assets/89889583/f07849c2-80b2-4dce-ba7e-76601615200c" width="75%"></p>

#### 2. 고려 사항
|주제|내용|
|----|----|
|예측 모델 분리 여부|곡선 선로 모델, 직선 선로 모델 2개의 모델 제작|
|변수 추가|yaw damper, 가속도, 수직하중, 편향력 관련 변수 생성|
|validation split|10000개 중 500개 행|
|CNN 학습 범위|3m, 5m, <strong>7m(선정)</strong>, 10m|
|activation|relu, swish, <strong>selu(선정)</strong>|
|optimizer|SGD, Adam, <strong>Nadam(선정)</strong>|


<br>

## 💻 기술 스택
<b> 언어 </b><br>
<span><img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white"></span><br>

<b> 라이브러리 </b><br>
<span><img src="https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white"></span>
<span><img src="https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"></span>
<span><img src="https://img.shields.io/badge/scikit_learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"></span>
<span><img src="https://img.shields.io/badge/tensorflow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white"></span>
<span><img src="https://img.shields.io/badge/keras-D00000?style=for-the-badge&logo=keras&logoColor=white"></span><br>

<b> 프로그래밍 인터페이스 </b><br>
<span><img src="https://img.shields.io/badge/googlecolab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white"></span>
