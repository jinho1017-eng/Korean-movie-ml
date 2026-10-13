# 🎬 한국 영화 관객 수 예측

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jinho1017-eng/korean-movie-audience-prediction/blob/main/korean_movie_audience_prediction.ipynb)

한국 박스오피스 데이터로 영화의 **전체 관객 수**를 예측하는 회귀 모델을 만들고, 여러 모델의 성능을 비교했습니다.

<br>

## 📌 프로젝트 요약

| 항목 | 내용 |
|---|---|
| 목표 | 영화 정보로 전체 관객 수(`audience_total`) 예측 |
| 데이터 | 한국 개봉 영화 20,730편 (2010.01 ~ 2025.04) |
| 모델 | Linear Regression, Decision Tree, Random Forest |
| 최종 모델 | **Random Forest (R² 0.9875)** |
| 사용 기술 | Python, pandas, NumPy, Matplotlib, scikit-learn, Google Colab |

<br>

## 📂 데이터

- **출처**: [Kaggle – Korean Box Office (2010–2025.04)](https://www.kaggle.com/datasets/kangminjung0405/korean-box-office-20102025-04)
- **원본**: 영화진흥위원회 KOBIS
- **파일**: `movie_box_office_kr_until_2025_0430.csv`

주요 변수: 개봉일, 제작 국가, 스크린 수, 서울 관객 수, 서울 매출액, 장르, 관람 등급, 영화 구분

<br>

## 🔍 분석 과정

1. **전처리**
   - 결측값 7건 제거
   - 예측에 쓰지 않는 변수 제거 (순위, 제목, 감독, 전체 매출액 등)
   - 개봉일 → 개봉 연도, 개봉 월로 분리
   - 범주형 변수 원-핫 인코딩
2. **탐색적 데이터 분석 (EDA)**
   - 관객 수 분포 확인 (로그 변환)
   - 스크린 수, 서울 관객 수와 전체 관객 수의 관계
   - 장르별, 관람 등급별 평균 관객 수
   - 변수 간 상관관계
3. **모델 학습 및 평가**
   - 학습 80% / 테스트 20% 분리
   - 3개 모델 학습 후 MAE, RMSE, R²로 비교
   - GridSearchCV로 Random Forest 하이퍼파라미터 튜닝

<br>

## 📊 결과

| 모델 | MAE | RMSE | R² |
|---|---:|---:|---:|
| Linear Regression | 28,992 | 98,837 | 0.9799 |
| Decision Tree | 17,276 | 106,414 | 0.9767 |
| **Random Forest** | **13,360** | **77,879** | **0.9875** |

- **Random Forest**가 모든 지표에서 가장 좋은 성능을 보였습니다.
- GridSearchCV로 찾은 최적 파라미터가 기본값과 같아서, 튜닝 후에도 성능은 같았습니다.

<br>

## 💡 배운 점 및 개선 방향

- 서울 관객 수와 전체 관객 수의 상관계수가 **0.99**로 매우 높습니다. 그래서 예측 정확도가 높게 나왔습니다.
- 서울 관객 수는 개봉 **후에** 알 수 있는 정보입니다. 개봉 **전** 흥행 예측을 하려면 이 변수를 빼고 장르, 등급, 스크린 수, 개봉 시기만으로 다시 학습해 볼 계획입니다.
- 관객 수 분포가 한쪽으로 크게 치우쳐 있으므로, 로그 변환한 값을 예측하는 방법도 시도해 보고 싶습니다.

<br>

## ▶️ 실행 방법

1. 위의 **Open In Colab** 버튼을 누릅니다.
2. 이 저장소의 `movie_box_office_kr_until_2025_0430.csv`를 내려받아 Colab에 업로드합니다.
3. **런타임 → 모두 실행**을 누릅니다.
