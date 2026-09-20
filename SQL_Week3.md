# 📘 SQL_BASIC 3주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 집계 함수와 `GROUP BY`, `HAVING`을 학습합니다.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_3rd_TIL

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-5. 집계(GROUP BY + HAVING + SUM/COUNT)

### 2-7. 정리

### 2-8. 새로운 집계 함수 소개(GROUP BY ALL, 2024-02-26에 나온 함수)

---

## ✨ 선택 강의

- 2-6. 연습 문제: 집계와 조건 조회를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | ✅ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | 🍽️ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | 🍽️ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | 🍽️ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념 정리

아래 키워드 중 중요하다고 생각한 개념을 2개 이상 골라 짧게 정리해주세요. 3개보다 더 많이 정리하고 싶다면 자유롭게 항목을 추가해도 좋습니다.

이번 주 키워드:
- COUNT
- SUM
- AVG
- MAX
- MIN
- GROUP BY
- HAVING
- 집계 기준

## 01.

```
개념 이름:  집계 함수
개념 설명:
- 집계는 여러 행의 데이터를 모아서 하나의 값으로 계산하는 과정이다.
  - **COUNT**는 **데이터의 개수를 계산**한다.
  - **SUM**은 **숫자형 값의 합계를 계산**한다.
  - **AVG**는 **숫자형 값의 평균을 계산**한다.
  - **MAX**는 **가장 큰 값**을, **MIN**은 **가장 작은 값**을 구한다.
  - **COUNT(*)**는 **행 전체의 개수를 세고**, **COUNT(컬럼명)**은 **해당 컬럼에서 NULL이 아닌 값의 개수를 센다**.
예시 쿼리:
<aside>
📌

```sql
SELECT
  COUNT(*) AS total_count,
  SUM(total) AS total_sum,
  AVG(total) AS average_total,
  MAX(total) AS maximum_total,
  MIN(total) AS minimum_total
FROM `프로젝트명.데이터세트명.pokemon`;
```

</aside>
  - `COUNT(*)`: 전체 포켓몬의 수
  - `SUM(total)`: 능력치 총합의 합계
  - `AVG(total)`: 능력치 총합의 평균
  - `MAX(total)`: 가장 높은 능력치 총합
  - `MIN(total)`: 가장 낮은 능력치 총합


```

## 02.

```
개념 이름: GROUP BY와 집계 기준
개념 설명:
- GROUP BY는 같은 값을 가진 데이터를 하나의 그룹으로 묶을 때 사용한다.
  - 데이터를 그룹으로 묶은 후 각 그룹에 COUNT, SUM, AVG 등의 집계 함수를 적용할 수 있다.
- 집계 기준은 어떤 컬럼을 기준으로 데이터를 묶어 계산할 것인지를 의미한다.
  - SELECT에서 집계 함수로 계산하지 않은 컬럼은 일반적으로 GROUP BY에 작성해야 한다.
예시 쿼리:
```
<aside>
📌

```sql
SELECT
  type1,
  COUNT(*) AS pokemon_count
FROM `프로젝트명.데이터세트명.pokemon`
GROUP BY type1;
```

</aside>
  - `type1`을 집계 기준으로 사용하여 같은 주 속성의 포켓몬을 하나의 그룹으로 묶었다.
  - `COUNT(*)`를 사용하여 각 속성에 해당하는 포켓몬의 수를 계산하였다.




# 2️⃣ 수행 인증란

아래 중 하나 이상을 첨부해주세요.

- 강의 수강 화면 캡처
- 문제 풀이 정답 화면 캡처
- SQL 실행 결과 화면 캡처

<img width="543" height="616" alt="image" src="https://github.com/user-attachments/assets/5a0b75b4-6bcb-4521-9a94-c1844b03a777" />



---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [최댓값 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59415)

풀이 과정:
1. 코드
SELECT
    MAX(DATETIME) AS 시간
FROM ANIMAL_INS;

2. 정답
   시간 2018-01-29 15:00:00

풀이
  - MAX(DATETIME): DATETIME 중 가장 큰 값, 즉 가장 최근의 보호 시작일을 조회
  - AS 시간: 결과의 컬럼 이름을 시간으로 표시
  - FROM ANIMAL_INS: 동물 정보를 가져올 테이블 지정

```
- 문제 요구사항: 동물 보호소에 가장 최근에 들어온 동물의 보호 시작일을 조회해야 한다.
- 사용한 SQL 절:  DATETIME 컬럼에서 가장 큰 날짜와 시간을 찾기 위해 MAX(DATETIME)을 사용하였다.
- 새로 배운 점: 날짜와 시간 데이터에도 MAX 함수를 사용할 수 있으며, 가장 큰 DATETIME 값은 가장 최근의 날짜와 시간을 의미한다는 점을 배웠다.
```


## 🧩 문제 2

문제 링크: [가장 비싼 상품 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131697)

풀이 과정:
1. 코드
SELECT
  MAX(PRICE) AS MAX_PRICE
FROM PRODUCT;

2. 정답
   MAX_PRICE 85000

```
- 사용한 집계 함수: 가장 큰 값을 구하는 MAX 함수를 사용하였다.
- 집계 대상 컬럼: 상품의 판매 가격이 저장된 PRICE 컬럼을 집계 대상으로 사용하였다.
- 결과를 검증한 방법: 실행 결과가 문제의 예시와 같은지 확인하고, 출력된 컬럼명이 MAX_PRICE로 표시되는지도 확인하였다.
```


## 🧩 문제 3

문제 링크: [고양이와 개는 몇 마리 있을까](https://school.programmers.co.kr/learn/courses/30/lessons/59040)

풀이 과정:
1. 코드
    SELECT
      ANIMAL_TYPE,
      COUNT(*) AS count
    FROM ANIMAL_INS
    GROUP BY ANIMAL_TYPE
    ORDER BY ANIMAL_TYPE;
2. 정답
| ANIMAL_TYPE | count |
| --- | --- |
| Cat | 2 |
| Dog | 1 |

```
- 그룹화 기준: 동물의 종류별로 마릿수를 계산하기 위해 ANIMAL_TYPE을 그룹화 기준으로 사용하였다.
- WHERE와 HAVING 중 사용한 절: 모든 동물을 종류별로 집계하는 문제이므로 별도의 조건이 필요하지 않아 WHERE와 HAVING을 사용하지 않았다.
- 처음 틀렸다면 틀린 이유: 틀리지는 않았지만, 고양이와 개를 구분하여 계산해야 하는 것을 데이터 분석이 처음이라면 헷갈렸을 수 있을 것 같다.
- 새로 배운 SQL 패턴: 범주별 개수를 구할 때 SELECT에 그룹화할 컬럼과 COUNT(*)를 작성하고, 같은 컬럼을 GROUP BY에 지정하는 패턴을 배웠다.
```

<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. -->

---

# 4️⃣ 이번 주 회고

```
1. 문제를 SQL로 옮길 때 가장 어려웠던 부분: 전체 데이터를 하나로 계산해야 하는지, 특정 컬럼을 기준으로 그룹을 나누어 계산해야 하는지 판단하는 부분은 헷갈렸다.
2. WHERE와 HAVING의 차이를 어떻게 이해했는지: WHERE는 GROUP BY로 데이터를 묶기 전에 개별 행에 조건을 적용하고, HAVING은 그룹화한 후 COUNT나 SUM과 같은 집계 결과에 조건을 적용한다고 이해하였다.
3. 다음 주에 더 연습하고 싶은 문제 유형: GROUP BY로 여러 그룹을 만들고 COUNT, SUM, AVG를 적용하는 문제를 더 연습하고 싶다.
```

수고하셨습니다!




