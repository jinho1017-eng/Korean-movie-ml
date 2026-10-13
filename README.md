🎬 한국 영화 관객 수 예측 (머신러닝)
한국 박스오피스 데이터를 이용해 영화의 전체 관객 수(audience_total) 를 예측하는 회귀 모델을 만들고, 여러 모델의 성능을 비교한 프로젝트입니다.

📂 데이터
출처: Kaggle – Korean Box Office (2010–2025.04)
원본: 영화진흥위원회 KOBIS (영화관입장권 통합전산망)
파일: movie_box_office_kr_until_2025_0430.csv
크기: 20,730개 영화 × 15개 변수 (2010년 1월 ~ 2025년 4월 30일 개봉작)
변수	설명
release_date	개봉일
format_type	영화 형식 (장편 등)
nation	제작 국가
screens_total	전체 스크린 수
audience_total	전체 관객 수 (예측 대상)
sales_seoul_krw	서울 매출액 (원)
audience_seoul	서울 관객 수
genre	장르
rating	관람 등급
film_class	영화 구분 (상업/독립 등)
🛠 사용 기술
Python, Google Colab
pandas, NumPy
Matplotlib
scikit-learn
🔍 분석 과정
데이터 불러오기 및 확인: 크기, 컬럼, 데이터 타입 확인
전처리
결측값 제거 (sales_seoul_krw 결측 7건)
예측에 불필요한 변수 제거 (rank, title, director, sales_total_krw, movie_type)
개봉일을 개봉 연도 / 개봉 월로 변환
범주형 변수 원-핫 인코딩 (get_dummies) → 입력 변수 103개
탐색적 데이터 분석 (EDA)
관객 수 분포 (로그 변환)
스크린 수, 서울 관객 수와 전체 관객 수의 관계
장르별, 관람 등급별 평균 관객 수
수치형 변수 간 상관관계
모델 학습: 학습 80% / 테스트 20% 분리
Linear Regression
Decision Tree
Random Forest
하이퍼파라미터 튜닝: GridSearchCV로 Random Forest 튜닝 (3-fold, MAE 기준)
최적 파라미터: n_estimators=100, max_depth=None, min_samples_split=2
📊 결과
모델	MAE	RMSE	R²
Linear Regression	28,992	98,837	0.9799
Decision Tree	17,276	106,414	0.9767
Random Forest	13,360	77,879	0.9875
Tuned Random Forest	13,360	77,879	0.9875
Random Forest가 세 가지 지표 모두에서 가장 좋은 성능을 보였습니다.
튜닝으로 찾은 최적 파라미터가 기본값과 같아서, 튜닝 전과 후의 성능이 같습니다.
💡 배운 점 및 개선 방향
서울 관객 수(audience_seoul)와 전체 관객 수의 상관계수가 0.99로 매우 높습니다. 그래서 R²가 높게 나온 것으로 보입니다.
서울 관객 수는 개봉 후에야 알 수 있는 정보입니다. 개봉 전 흥행 예측 모델을 만들려면 이런 변수를 빼고 장르, 등급, 스크린 수, 개봉 시기만으로 다시 학습해 볼 계획입니다.
관객 수 분포가 한쪽으로 크게 치우쳐 있으므로, 로그 변환한 값을 예측 대상으로 쓰는 방법도 시도해 볼 수 있습니다.
▶️ 실행 방법
위 Kaggle 링크에서 csv 파일을 내려받습니다.
노트북(.ipynb)을 Google Colab에서 엽니다.
csv 파일을 Colab에 업로드하고 셀을 순서대로 실행합니다.
