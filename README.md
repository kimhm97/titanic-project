# Titanic 생존 예측 프로젝트

## 1. 프로젝트 개요

타이타닉 승객 데이터를 활용하여 생존 여부를 예측하고,  
EDA와 통계적 검정을 통해 **생존에 영향을 주는 주요 변수**를 도출하였다.

또한, Feature Engineering이 실제 모델 성능에 어떤 영향을 주는지 검증하였다.

분석 목적:
- 단순 예측이 아니라 **“왜 이 변수가 중요한지”를 설명하는 것에 집중**

---

## 2. 문제 정의

- 승객 정보로 생존 여부를 예측할 수 있는가?
- 어떤 변수가 생존에 가장 큰 영향을 주는가?
- Feature Engineering이 실제 성능 개선으로 이어지는가?

---

## 3. 데이터 개요

- Kaggle Titanic Dataset
- Train: 891 / Test: 418

---

## 4. 분석 과정

### 4.1 EDA

- Fare → 강한 양의 왜도 → 로그 변환 필요 판단
- Cabin → 결측률 높음 → 직접 사용 제외
- Sex, Pclass → 생존률 차이 명확 → 주요 변수 후보 선정

결과:
→ **변수 중요도 후보를 선별**

---

### 4.2 통계적 검정

#### 범주형 (카이제곱)
- 대부분 변수에서 유의한 차이 확인
- 특히 **Sex, Pclass → 영향력 큼**

결과:
→ **주요 변수: Sex, Pclass**

---

#### 수치형 (t-test)
- Fare, Age 모두 유의
- 특히 Fare → 집단 간 차이 큼

결과:
→ **Fare → 주요 feature로 사용**

---

## 5. Feature Engineering

다음 변수 생성:

- Title
- FamilySize
- IsAlone
- AgeBand / FareBand
- CabinDeck / TicketPrefix

결과:
- Title, FamilySize → 성능 개선에 기여
- AgeBand, FareBand → 효과 제한적

정리:
→ **모든 파생변수가 유의미한 것은 아님을 확인**

---

## 6. 모델링

- Logistic Regression
- Decision Tree
- RandomForest
- Gradient Boosting

평가:
- Stratified K-Fold
- F1 Score 기준 비교

---

## 7. 결과

- 최종 모델: RandomForest
- 평균 F1 Score: 0.7715

결과 해석:

- Feature Engineering 적용 후 성능 개선 확인
- 특히 EDA 기반 변수 선택이 성능에 직접 영향

---

## 8. 예측 결과 (Sanity Check)

- 예측 분포
  - 사망(0): 63.16%
  - 생존(1): 36.84%

- 실제 데이터 분포 (train)
  - 사망(0): 61.62%
  - 생존(1): 38.38%

해석:
- 실제 데이터 분포와 유사한 비율을 보이며, 특정 클래스에 과도하게 치우치지 않은 정상적인 예측 결과로 판단된다.

---

## 9. 주요 인사이트

- 여성 승객의 생존 확률이 높음
- 객실 등급이 높을수록 생존 확률 증가
- 요금(Fare)은 생존과 강한 상관관계 존재
- 가족 관련 변수(FamilySize, IsAlone)가 중요한 역할 수행
- Feature Engineering이 모델 성능 향상에 중요한 역할 수행

---

## 10. 한계

- 데이터 수 제한 → 일반화 한계
- Cabin, Age 결측 → 정보 손실

---

## 11. 개선 방향

- 변수 선택 기준을 EDA 기반으로 재정리
- 왜도 및 이상치 처리 방식 개선
- 분석 과정 중심으로 모델 개선 시도

---

## 12. 사용 기술

- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib, Seaborn

---

## 13. 프로젝트 구조
"""
titanic-project/
├─ data/
│ ├─ raw/
│ ├─ interim/
│ └─ processed/
│
├─ output/
│ ├─ tables/
│ ├─ figures/
│ └─ submissions/
│
├─ notebook/
│ ├─ 01_EDA/
│ ├─ 02_preprocessing/
│ └─ 03_model/
│
├─ reports/
│ └─ summary.ipynb
│
└─ README.md
"""


---

## 14. 결론

본 프로젝트를 통해 단순한 모델 성능 향상보다,  
데이터를 이해하고 EDA를 통해 변수의 특성을 파악하는 과정이 중요하다는 것을 확인하였다.

또한 Feature Engineering을 통해 모델 성능이 개선되는 과정을 경험하며,  
데이터 전처리와 변수 생성이 모델링에 큰 영향을 미친다는 점을 학습하였다.

이를 통해 모델 결과를 단순히 사용하는 것이 아니라,  
분석 과정과 연결하여 해석하는 능력이 중요하다는 것을 확인하였다.
