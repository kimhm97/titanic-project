# Titanic 생존 예측 프로젝트

## 1. 프로젝트 개요

본 프로젝트는 타이타닉 승객 데이터를 활용하여 생존 여부를 예측하고,
데이터 분석을 통해 생존에 영향을 미치는 주요 요인을 도출하는 것을 목표로 한다.

단순 예측을 넘어서 다음과 같은 전체 분석 프로세스를 수행하였다.

* 탐색적 데이터 분석(EDA)
* 통계적 검정
* Feature Engineering
* 모델 학습 및 성능 비교
* 결과 해석

---

## 2. 문제 정의

* 승객의 특성(성별, 나이, 객실 등급 등)을 활용하여 생존 여부를 예측
* 생존에 영향을 미치는 주요 변수 도출
* Feature Engineering이 모델 성능에 미치는 영향 검증

---

## 3. 데이터 개요

* 데이터 출처: Kaggle Titanic Dataset
* 학습 데이터: 891건
* 테스트 데이터: 418건

주요 변수:

* Pclass (객실 등급)
* Sex (성별)
* Age (나이)
* Fare (요금)
* SibSp / Parch (가족 관련 변수)
* Cabin, Embarked

---

## 4. 탐색적 데이터 분석 (EDA)

### 4.1 단변량 분석

* Fare는 강한 오른쪽 치우침을 보여 로그 변환 필요
* Cabin은 결측 비율이 매우 높아 직접 활용이 어려움

### 4.2 이변량 분석

* 성별(Sex), 객실 등급(Pclass), 요금(Fare)에 따라 생존률 차이가 명확하게 나타남
* Age는 일부 패턴이 존재하나 영향은 상대적으로 제한적

---

## 5. 통계적 검정

### 5.1 범주형 변수 (카이제곱 검정)

* Sex, Pclass, FareBand에서 통계적으로 유의한 차이 확인

### 5.2 수치형 변수 (Welch t-test)

* Fare, Age에서 유의한 차이 확인
* 특히 Fare가 더 큰 영향력을 보임

---

## 6. Feature Engineering

다음과 같은 파생변수를 생성하였다.

* Title: 이름에서 호칭 추출
* FamilySize: 가족 수
* IsAlone: 단독 탑승 여부
* AgeBand / FareBand: 구간화 변수
* CabinDeck / TicketPrefix: 문자열 기반 패턴 추출

분석 결과:

* Title, FamilySize는 모델 성능 향상에 기여
* AgeBand, FareBand는 성능 기여도가 제한적

---

## 7. 모델링

### 7.1 사용 모델

* Logistic Regression
* Decision Tree
* RandomForest
* Gradient Boosting

### 7.2 평가 방법

* Stratified K-Fold 교차검증
* F1 Score를 기준으로 모델 성능 비교

---

## 8. 결과

* 최종 모델: RandomForest
* 선택된 Feature Set: derived_features_only
* 평균 F1 Score: 0.7715

Feature Engineering을 통해 모델 성능이 개선됨을 확인하였다.

---

## 9. 예측 결과 분석

테스트 데이터 예측 결과:

* 사망(0): 약 63%
* 생존(1): 약 37%

이는 실제 데이터 분포와 유사하며, 모델이 안정적으로 동작하고 있음을 의미한다.

---

## 10. 주요 인사이트

* 여성 승객의 생존 확률이 높음
* 객실 등급이 높을수록 생존 확률 증가
* 요금(Fare)은 생존과 강한 상관관계 존재
* 가족 관련 변수(FamilySize, IsAlone)가 중요한 역할 수행
* Feature Engineering이 모델 성능 향상에 핵심적 역할 수행

---

## 11. 한계 및 개선 방향

* 데이터 수가 제한적이므로 일반화에 한계 존재
* 일부 변수(Cabin, Age)의 결측 비율이 높음
* 향후 개선 방향:

  * 하이퍼파라미터 튜닝
  * 추가 모델 적용 (XGBoost, LightGBM 등)

---

## 12. 사용 기술

* Python
* Pandas, NumPy
* Scikit-learn
* Matplotlib, Seaborn

---

## 13. 프로젝트 구조

```id="korean_struct"
titanic-project/
├─ data/
├─ output/
├─ notebook/
├─ reports/
└ README.md
```

---

## 14. 결론

본 프로젝트를 통해 데이터 분석에서 단순한 모델 성능보다
EDA와 Feature Engineering이 더욱 중요한 역할을 한다는 것을 확인하였다.

또한 모델 결과를 해석하고 분석 과정과 연결하는 능력이
실무에서 중요한 역량임을 확인하였다.
