# <a href="https://aifactory.space/task/2511/overview" target="_blank">2023 제1회 철도 인공지능 경진대회</a>
## 🚩 대회 정보
- 주제 : 열차의 주행 안정성 진단에 사용되는 ‘탈선계수’를 보다 높은 정확도로 예측할 수 있는 인공지능 모델 개발
- 기간 : 23.08.01 ~ 23.09.21
- 팀명 : 한국철도999 (총 4명)
- 결과 : 5위 / 68팀 (78.681525점)
- 수상 : 장려상🥉
<br>

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
