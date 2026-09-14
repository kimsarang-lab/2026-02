# 📘 SQL_BASIC 2주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 저장된 데이터를 확인하는 방법과 `SELECT`, `FROM`, `WHERE`의 기본 구조를 학습합니다.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_2nd_TIL

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-2. 저장된 데이터 확인하기(데이터베이스, 데이터 웨어하우스, ERD)

### 2-3. 데이터 탐색(SELECT, FROM, WHERE)

---

## ✨ 선택 강의

- 2-4. SELECT 연습 문제: SELECT, FROM, WHERE를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | 🍽️ |
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
- SELECT
- FROM
- WHERE
- 조건식
- ORDER BY
- LIMIT
- 테이블 구조 확인

## 00.

```
개념 이름: 데이터 웨어하우스(Data Warehouse)
개념 설명: 여러 곳에서 수집한 데이터를 분석하기 쉽도록 통합하여 저장하는 공간
- 일반적인 데이터베이스가 데이터의 입력·수정·삭제와 같은 업무 처리에 집중한다면, 데이터 웨어하우스는 대량의 데이터를 조회하고 분석하는 데 주로 사용된다.
- BigQuery는 대규모 데이터를 저장하고 SQL로 분석할 수 있는 데이터 웨어하우스이다.
```

## 01.

```
개념 이름: SELECT와 FROM
개념 설명:
- SELECT는 테이블에서 확인하고 싶은 열(컬럼)을 선택할 때 사용한다.
  - 여러 열을 선택할 때는 열 이름을 쉼표(,)로 구분한다.
  - 모든 열을 확인하려면 열 이름 대신 *(별표)를 사용할 수 있다.
- FROM은 데이터를 가져올 테이블을 지정할 때 사용한다.
  - BigQuery에서는 일반적으로 `프로젝트명', '데이터세트명', '테이블명`의 순서로 테이블의 위치를 작성한다.
예시 쿼리:
  SELECT
    id,
    kor_name,
    type1
  FROM `프로젝트명.데이터세트명.pokemon`;
```

## 02.

```
개념 이름: WHERE와 조건식
개념 설명:
  - WHERE는 테이블에서 특정 조건을 만족하는 행만 추출할 때 사용한다.
  - 조건식에는 =, !=, >, <, >=, <= 등의 비교 연산자를 사용할 수 있다.
  - 문자형 값은 작은따옴표(' ')로 감싸고, 숫자형 값은 일반적으로 작은따옴표 없이 작성한다.
  - 여러 조건을 모두 만족해야 할 때는 AND를 사용한다.
  - 여러 조건 중 하나 이상을 만족하면 될 때는 OR를 사용한다.
예시 쿼리:
  SELECT
    id,
    kor_name,
    type1
  FROM `프로젝트명.데이터세트명.pokemon`
  WHERE type1 = 'Fire';
```



# 2️⃣ 수행 인증란

아래 중 하나 이상을 첨부해주세요.

- 강의 수강 화면 캡처
<img width="603" height="836" alt="image" src="https://github.com/user-attachments/assets/43a8a419-12cf-421e-a1ef-ffbe675e8541" />
<img width="1350" height="839" alt="image" src="https://github.com/user-attachments/assets/2b6b54e2-ddff-4558-ad2d-cd894f62548c" />
<img width="1335" height="834" alt="image" src="https://github.com/user-attachments/assets/99e86e3f-afd5-491f-9f9a-112c79dd2ffd" />



---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [모든 레코드 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/59034)

풀이 과정:

```
<aside>
💡

**코드**

  SELECT *
  FROM ANIMAL_INS
  ORDER BY ANIMAL_ID;

</aside>

- 테이블에서 확인한 컬럼:
    ANIMAL_ID, ANIMAL_TYPE, DATETIME, INTAKE_CONDITION, NAME, SEX_UPON_INTAKE 컬럼을 확인하였다.
- SELECT와 FROM을 작성한 방식:
    SELECT와 FROM을 작성한 방식: 모든 컬럼을 조회하기 위해 SELECT 뒤에 *를 작성하고, 데이터를 가져올 ANIMAL_INS 테이블을 FROM 뒤에 작성하였다.
- 새로 배운 점:
    SELECT *를 사용하면 테이블의 모든 컬럼을 조회할 수 있고, ORDER BY를 사용하면 지정한 컬럼을 기준으로 결과를 정렬할 수 있다는 점을 배웠다.
```


## 🧩 문제 2

문제 링크: [아픈 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59036)

풀이 과정:

```
<aside>
💡

**코드**

  SELECT
      ANIMAL_ID,
      NAME
  FROM ANIMAL_INS
  WHERE INTAKE_CONDITION = 'Sick'
  ORDER BY ANIMAL_ID;

</aside>
- 문제에서 요구한 조건: 보호소에 들어올 당시 상태가 아픈 동물의 아이디와 이름을 조회해야 한다.
- WHERE 절로 옮긴 방식: 아픈 동물은 INTAKE_CONDITION 값이 Sick인 경우이므로, WHERE INTAKE_CONDITION = 'Sick'으로 작성하였다.
- 정렬 기준이 있다면 사용한 기준: 결과를 동물의 아이디 순으로 조회하기 위해 ORDER BY ANIMAL_ID를 사용하였다
- 새로 배운 점:  WHERE 절을 사용하면 특정 조건에 해당하는 행만 추출할 수 있으며, Sick과 같은 문자형 값을 조건으로 사용할 때는 작은따옴표로 감싸야 한다는 점을 배웠다.
```



---

# 4️⃣ 이번 주 회고

```
1. SELECT, FROM, WHERE 중 가장 헷갈린 개념:
  아직 SQL 문법이 익숙하지 않아 무엇이 헷갈리는지 명확하게 구분하기는 어렵지만, 세 개념을 다음과 같이 정리하였다.
      - SELECT: 조회하고 싶은 열을 선택한다.
      - FROM: 데이터를 가져올 테이블을 지정한다.
      - WHERE: 조건에 맞는 행을 선택한다.
  
2. 문제를 풀 때 가장 자주 확인하게 된 부분:
  테이블명과 변수명이 정확한지 확인 하는 것을 가장 중요하게 보았다.
  특히 문자형 조건을 작성할 때 작은따옴표를 빠뜨리지 않았는지도 확인하였다.
3. 다음 주 문제 풀이에서 의식하고 싶은 습관:
  바로 쿼리를 작성하기보다 먼저 어떤 테이블에서 어떤 열과 행을 가져올 것인지 생각한 후 SELECT, FROM, WHERE 순서로 작성하는 습관을 들이고 싶다.
```

수고하셨습니다!




