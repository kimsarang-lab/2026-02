# 📘 모델 학습 시 고려사항 가이드 📘 

모델이 우수한 성능을 낸다고 하더라도, 그 이유를 분석가/사이언티스트가 이해하지 못한다면 결코 의미 있지 않습니다.

👉 **코드를 짜는 시간보다 고민하는 데 더 많은 시간을 할애하세요.**

👉 **결과에 휘둘리기보다, 본인의 논리를 세우고 검증하는 습관**을 들이세요. 예상과 다르다면 다시 학습해가면 됩니다.

> 모든 부분에 힘을 주실 필요는 없습니다. 핵심 포인트에 집중하세요.

---

## 1️⃣ 결측치 처리

- 결측치를 확인하고 적절한 방식으로 대체해야 합니다.
- 대체 방식: 평균, 중앙값, 최빈값, 혹은 도메인 지식 기반의 값.

> **실습**
><img width="855" height="562" alt="image" src="https://github.com/user-attachments/assets/c984473d-a083-4381-87d2-2751a76d7399" />

> - 시각화를 통해 결측치 확인
### 결과
*   Age 컬럼은 변동성 있는 결측치가 듬성듬성 있음
*   Cabin 컬럼은 모든 열의 면적들이 결측치로 구성되어 있음
*   Embarked 컬럼은 열의 초기 행들에 소수의 결측치가 있음


참고)
<img width="491" height="382" alt="image" src="https://github.com/user-attachments/assets/b1334231-c05f-49f1-a4a1-405dd8cd76d6" />

> - 대체 방법과 그 이유를 논리적으로 설명하기
1. Age: ori_train.head() 으로 데이터 구조를 확인 했을 때, age 값은 연속형 변수임. 결측값 비율은 19.87%(n=177)으로 확인 되었음.
Age 분포는 오른쪽 꼬리가 조금 더 긴 우측 편향 분포(right-skewed distribution)를 보임. 아래의 그래프에 따르면 평균이 29.7세, 중앙값이 28.0세이므로 평균이 중앙값 큼. 비교적 나이가 많은 승객들이 평균을 오른쪽으로 끌어올린 것으로 해석할 수 있음. 이 경우에는 Age 결측치를 중앙값 28세로 대체하는 것이 적절함. 하지만 평균과 중앙값의 차이가 1.7세 정도라서 심한 우측 편향은 아니고 약한 우측 편향에 가까움.

<img width="703" height="482" alt="image" src="https://github.com/user-attachments/assets/00fb40fe-c4d3-42e3-9295-9e021c6197a1" />

2. Cabin
Cabin 변수는 전체 891명 중 687명(77.1%)이 결측으로, 결측 비율이 매우 높았음(그림 1). 객실정보의 기록 여부가 승객 등급(Pclass)과 관련되어 있을 가능성을 확인하기 위해, 객실 등급별 Cabin 변수의 결측률을 비교하였음(그림 2). 분석 결과, 1등석 승객의 Cabin 결측률은 약 18%로 낮았지만, 2등석과 3등석 승객의 결측률은 각각 약 91%, 98%로 매우 높게 나타남. 따라서 Cabin의 결측은 모든 승객에게 무작위로 발생했다기보다 승객 등급과 관련된 체계적인 결측일 가능성이 있음. 따라서 Cabin 변수를 단순 삭제하거나 최빈값으로 대체하기보다 객실정보의 기록 여부 자체를 하나의 정보로 활용하는 방안을 생각함.
-> 객실정보가 기록된 경우를 1, 결측인 경우를 0으로 코딩한 CabinKnown 변수를 생성하여, 결측이 많은 문자열 변수를 단순한 이진 변수로 변환하고, Cabin 변수를 삭제하더라도 객실정보의 유무에 포함된 정보를 보존하고자 함. 


(1)
<img width="675" height="481" alt="image" src="https://github.com/user-attachments/assets/60fa3059-cd07-4437-8b6f-19f79fcdd1b2" />

(2)
<img width="746" height="480" alt="image" src="https://github.com/user-attachments/assets/21133a2e-e55f-40a6-b9e2-8c33766028c5" />

3. Embarked
Embarked는 승객의 탑승 항구를 나타내는 명목형 범주형 변수이며, 전체 891명 중 2명(0.22%)에서 결측치가 확인되었음. 범주형 변수에는 평균이나 중앙값을 적용할 수 없으므로 가장 빈도가 높은 범주를 확인하였다. 그 결과 S가 644명으로 가장 많아 최빈값으로 나타남. 결측치의 비율이 매우 낮아 최빈값 대체가 전체 분포에 미치는 영향이 제한적이라고 판단하여, 결측값을 훈련 데이터의 최빈값인 S로 대체하는 방안을 생각함. 
   <img width="708" height="477" alt="image" src="https://github.com/user-attachments/assets/1a9b3c9a-e3c1-4769-8b50-426c7c54f9a9" />


## 2️⃣ 데이터 인코딩

범주형 변수는 모델이 이해할 수 있는 숫자형으로 변환해야 합니다.

- **Label Encoding**: 순서가 있는 경우
- **One-Hot Encoding**: 순서가 없는 경우
- **Target Encoding**: 타겟 변수 평균/비율 기반



> **실습**
> - 어떤 컬럼에 어떤 인코딩 방법을 썼는지
  >Sex, Embarked, Deck은 범주 사이에 순서가 없으므로 One-Hot Encoding을 적용하였다.
        Sex: 남성과 여성 사이에 순서가 없으므로 One-Hot Encoding
        Embarked: 탑승항구 C, Q, S 사이에 순서가 없으므로 One-Hot Encoding
        Deck: 객실구역 A, B, C 등의 범주 사이에 명확한 순서가 없으므로 One-Hot Encoding
        Pclass: 1등석, 2등석, 3등석의 순서가 있고 이미 숫자로 표현되어 있어 기존 값을 유지
        CabinKnown: 객실정보 유무가 이미 0과 1로 표현되어 있어 별도로 인코딩하지 않음
>   
> - 고려한 다른 방법과 선택하지 않은 이유
Label Encoding은 각 범주를 하나의 숫자로 변환하는 방법이지만, Sex, Embarked, Deck과 같이 순서가 없는 변수에 적용하면 모델이 범주 사이에 순서가 있다고 잘못 인식할 수 있어 사용하지 않았음

Target Encoding은 각 범주의 생존율을 이용하여 값을 변환하는 방법이지만, Survived의 정보를 인코딩에 사용하므로 데이터 누수와 과적합이 발생할 가능성이 있어 이번 분석에서는 사용하지 않았음.

Name, Ticket, Cabin은 서로 다른 값의 종류가 많아 One-Hot Encoding을 적용하면 변수가 지나치게 많이 생성될 수 있으므로 제외함. 


## 3️⃣ 데이터 스케일링

- 데이터 분포를 모델링에 적합하게 변환하기 위해 필요.
- 예: MinMaxScaler, StandardScaler, RobustScaler



> **실습**
> - 정규화 필요성 논의
로지스틱 회귀, KNN, SVM 등 변수의 크기나 거리에 영향을 받는 모델에서 특정 변수가 과도한 영향을 미치게 할 수 있음. 따라서 연속형 변수인 Age와 Fare의 범위를 조정할 필요가 있다고 판단하였음.

> - 선택한 스케일링 방법과 이유 설명
  Age와 Fare에 RobustScaler를 적용하였음. Fare는 일부 승객의 요금이 매우 높고 오른쪽으로 치우친 분포를 보이므로, 최솟값과 최댓값을 사용하는 MinMaxScaler나 평균과 표준편차를 사용하는 StandardScaler보다 이상치의 영향을 적게 받는 RobustScaler가 적절하다고 판단함. 
<br>

## 4️⃣ 데이터 왜도 (Skewness)

- 비대칭 분포는 성능 저하를 유발
- 변환 방법: 로그 변환, Box-Cox 변환 등



> **실습**
> - 각 컬럼 분포 시각화
수치형 변수 중 연속형 변수인 Age와 Fare, 계수형 변수인 SibSp와 Parch의 분포를 시각화하고 왜도를 산출함. 그 결과 Fare, SibSp, Parch의 왜도 절댓값이 1 이상으로 나타나 강한 우측 편향을 보임. Fare는 일부 고액 요금으로 인해 왜도가 크게 나타남. 
<img width="846" height="566" alt="image" src="https://github.com/user-attachments/assets/a31f4b01-5107-48b3-aa4f-f86f8aa01a53" />

> - 왜도 수치 계산
**code**
            skewness_values = (
                train_clean[skew_columns]
                .skew()
                .sort_values(ascending=False)
            )
            
            print(skewness_values)
**Results**           
    Fare     4.787317
    SibSp    3.695352
    Parch    2.749117
    Age      0.510245
    dtype: float64

> - 타이타닉 데이터셋 예시 → 어떤 컬럼이 왜도 처리 필요한지?
(1) Fare: 로그 변환 적용
  Fare는 왜도가 4.787로 가장 높고, 그래프에서도 오른쪽 꼬리가 매우 길게 나타남. 일부 승객이 매우 높은 요금을 지불했기 때문에 대부분의 승객이 낮은 값에 몰리고 일부 큰 값이 오른쪽 꼬리를 만든 것으로 추측할 수 있음. 따라서 Fare는 log1p() 변환을 적용하는 것이 적절할 것으로 판단함.

(2) SibSp와 Parch
SibSp와 Parch도 높은 우측 왜도를 확인하였음. 하지만 SibSp와 Parch는 가족 수를 나타내는 이산형 계수 변수로서 0에 값이 집중되는 것이 변수의 자연스러운 특성임. 이에 실제 왜도 변환은 연속형 변수이면서 강한 우측 편향을 보인 Fare에만 적용함. 대신, SibSp와 Parch는 개별적으로 로그 변환하지 않고 승객 본인을 포함한 FamilySize 변수로 통합하였음.

<br>

## 5️⃣ 이상치 (Outliers)

- 이상치는 모델에 부정적 영향을 줄 수 있음
- 처리 방법: 제거, 대체(중앙값 등)



> **실습**
> - 이상치 기준을 제시
<img width="844" height="274" alt="image" src="https://github.com/user-attachments/assets/994b2a4b-c100-4556-a949-ea0967c1cecf" />

이상치 기준
          def detect_outliers_iqr(data, column):
          
              # 1사분위수와 3사분위수
              Q1 = data[column].quantile(0.25)
              Q3 = data[column].quantile(0.75)
          
              # 사분위범위
              IQR = Q3 - Q1
          
              # 이상치 기준
              lower_bound = Q1 - 1.5 * IQR
              upper_bound = Q3 + 1.5 * IQR
          
              # 기준을 벗어난 행
              outliers = data[
                  (data[column] < lower_bound)
                  | (data[column] > upper_bound)
              ]
          
              return {
                  'variable': column,
                  'Q1': Q1,
                  'Q3': Q3,
                  'IQR': IQR,
                  'lower_bound': lower_bound,
                  'upper_bound': upper_bound,
                  'outlier_count': len(outliers),
                  'outlier_percentage': len(outliers) / len(data) * 100
              }
> - 처리 여부와 이유 설명
(1) Age
IQR 기준에서는 2.5세 미만이거나 54.5세를 초과한 승객 66명이 이상치로 분류되었음. 하지만 하지만 영유아와 55세 이상의 승객은 충분히 실제로 존재할 수 있으므로, 삭제하지 않기로 결정함.

(2) Fare
Fare는 65.63보다 큰 값 116개가 이상치 후보로 확인 되었으나, 고액 요금은 1등석 승객에게서 실제로 발생할 수 있는 값으로 추정되어 삭제하지 않음.

(3) Family Size
FamilySize의 상한은 3.5로 계산됐으므로 실제로는 가족 규모가 4명 이상인 승객 91명이 이상치로 분류되었으나, 4인 이상 가족은 비현실적인 값임. 따라서 따로 처리 하지 않음.



## **6️⃣ 피처 선택 및 생성**

- **Feature Selection**: 불필요한 변수 제거 → 과적합 방지
- **Feature Engineering**: 새로운 변수 생성 (예: 곱셈/나눗셈으로 새로운 특징)



> **실습**
>
> - 새로 만든 피처가 있다면 설명하기
    FamilySize: 본인을 포함한 전체 동승 가족 수
>       FamilySize는 동승한 형제자매 및 배우자 수(SibSp)와 부모 및 자녀 수(Parch)에 승객 본인 1명을 더하여 산출한 전체 동승 가족 수
    CabinKnown: 객실정보 기록 여부
>       CabinKnown은 객실정보가 기록된 경우 1, 기록되지 않은 경우 0으로 코딩한 변수

 ** 제거한 변수
    -SibSp와 Parch는 새롭게 생성한 FamilySize와 정보가 중복되므로 제거
> - 다중공선성 여부 확인 & 처리 방법 제시
>  SibSp와 Parch를 제거한 후 모든 예측변수의 VIF가 2 미만으로 나타났으므로, 다중공선성 문제는 해결된 것으로 판단할 수 있음.
<img width="230" height="194" alt="image" src="https://github.com/user-attachments/assets/c06c3d46-cee0-4b64-a47e-b9d4e74611bc" />

*** 판단 결과 ***
    VIF가 5 미만: 다중공선성 문제가 크지 않음
    VIF가 5 이상: 다중공선성 가능성 검토
    VIF가 10 이상: 심각한 다중공선성 가능성
    VIF가 inf: 다른 변수와 완전한 선형관계

<br>


## **7️⃣ 데이터 분할**

- 훈련/검증/테스트 데이터 분할
- 일반적으로 **70~80% → 훈련 / 나머지 → 검증·테스트**



> **실습**
>
> - K-Fold vs Stratified K-Fold 학습
>     K-Fold: 전체 자료를 K개의 부분으로 나누고, 각각을 한 번씩 검증 데이터로 사용하는 방법
>     Stratified K-Fold: K-Fold와 동일하게 반복하지만, 각 Fold에서 종속변수의 범주 비율을 유지
>   
> - 최종적으로 어떤 방법을 썼는지, 이유 설명
    K-Fold의 Fold별 생존율은 33.57~41.26%로 최대 7.69%p의 차이를 보였으나, Stratified K-Fold에서는 38.03~38.73%로 최대 차이가 0.70%p에 불과함. 따라서 각 Fold에서 생존자와 사망자의 비율을 안정적으로 유지할 수 있는 5-Fold Stratified K-Fold를 최종 교차검증 방법으로 선택함.


## 8️⃣ 모델 선택

- 데이터 특성에 맞는 모델 선정
  - 선형 관계 → 선형 회귀
  - 비선형 관계 → 트리 기반 모델 등



> **실습**
>
> - 예측하고자 하는 값의 유형에 따른 모델 선정 논리 제시
> -   본 분석의 종속변수인 Survived는 사망(0)과 생존(1)으로 구분되는 이진 범주형 변수이므로 이진 분류모델을 사용
> -   승객의 생존은 성별, 연령, 객실 등급, 요금, 동승 가족 수 등 여러 요인이 복합적으로 작용하며, 각 독립변수와 생존 여부 간의 관계가 단순한 선형관계라고 보기 어려움.
> -   이에 비선형 관계와 변수 간 상호작용을 반영할 수 있고 이상치의 영향을 상대적으로 적게 받는 랜덤 포레스트 분류모델을 선택함.
> - 대안 모델 추천 가능
>     대안으로 로지스틱 회귀를 고려할 수 있다. 로지스틱 회귀는 각 독립변수가 생존 가능성에 미치는 영향을 회귀계수와 오즈비로 해석할 수 있다는 장점이 있음. 그러나 독립변수와 생존 여부 간의 관계를 기본적으로 선형적인 로짓 관계로 가정하므로 복잡한 비선형 관계와 변수 간 상호작용을 반영하는 데 제한이 있음.



- **하이퍼파라미터 튜닝**:

  Grid Search, Random Search 등으로 성능 최적화
<br>


## 9️⃣ 모델 평가

- 회귀: **MSE, MAE, R²**
- 분류: **Accuracy, Precision, Recall, F1-score**
- 교차 검증으로 일반화 성능 평가



> **실습**
>
> - 어떤 지표를 선택했는지와 그 이유 설명
>Accuracy, Precision, Recall, F1-score 및 ROC-AUC를 평가 지표로 사용
      > - Accuracy는 전체적인 예측 정확도를 확인하기 위해 사용하였으며, Precision과 Recall은 생존자 예측의 정확성과 실제 생존자 탐지 성능을 각각 확인하기 위해 사용함.
      > - F1-score를 통해 Precision과 Recall을 종합적으로 평가하였다. 주요 모델 선택 지표로는 특정 분류 기준값에 의존하지 않고 생존자와 사망자를 구분하는 전반적인 판별력을 평가할 수 있는 ROC-AUC를 사용함.
> - <img width="634" height="488" alt="image" src="https://github.com/user-attachments/assets/c1d9198a-069c-4e25-9aba-73342ce6b2bb" />
<img width="765" height="592" alt="image" src="https://github.com/user-attachments/assets/ea9a526b-634d-4ce0-8148-c246a16a6f61" />


<br>


## 🔟 과적합 방지

- **정규화**: L1, L2 규제로 복잡도 조절
- **Dropout**: 신경망에서 일부 노드 무작위 제거
- **Early Stopping**: 검증 성능이 개선되지 않으면 조기 종료



> **실습**
>
> - 과적합 방지를 위해 사용한 방법
> - 방법의 원리와 장점 설명




📌 **출처**: 4기 교육팀장님

