# 📘 SQL_BASIC 6주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 SQL 입문 과정의 핵심 고비인 `JOIN`을 학습합니다.

JOIN은 여러 테이블을 연결해서 분석 질문에 답하기 위해 반드시 필요한 개념입니다. 이번 주 과제에서는 정답 코드뿐 아니라 **어떤 테이블을 어떤 키로 연결했는지**를 꼭 기록해주세요.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_6th_TIL

### 섹션 6. 다량의 자료를 연결 : JOIN

### 5-2. JOIN 이해하기

### 5-3. 다양한 JOIN 방법

### 5-4. JOIN 쿼리 작성하기

### 5-5. JOIN을 처음 공부할 때 헷갈리는 부분

---

## ✨ 선택 강의

- 5-6. JOIN 연습문제: JOIN 문제를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | ✅ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | ✅ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | ✅ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | ✅ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념 정리

아래 키워드 중 중요하다고 생각한 개념을 2개 이상 골라 짧게 정리해주세요. 3개보다 더 많이 정리하고 싶다면 자유롭게 항목을 추가해도 좋습니다.

이번 주 키워드:
- JOIN
- INNER JOIN
- LEFT JOIN
- JOIN key
- alias
- NULL
- 다중 JOIN


01.
개념 이름: JOIN과 JOIN key

개념 설명:
- JOIN은 서로 다른 테이블에 저장된 데이터를 하나의 결과로 연결하는 방법이다.
- 테이블을 연결할 때 공통으로 가지고 있는 컬럼을 JOIN key로 사용한다.
- JOIN key를 잘못 지정하면 관계없는 데이터가 연결되거나 결과 행이 예상보다 많아질 수 있다.
- 두 테이블에 같은 이름의 컬럼이 있다면 테이블 별칭을 붙여 어느 테이블의 컬럼인지 표시하는 것이 좋다.

예시 쿼리:

SELECT
    B.BOOK_ID,
    A.AUTHOR_NAME
FROM BOOK AS B
JOIN AUTHOR AS A
    ON B.AUTHOR_ID = A.AUTHOR_ID;

- 연결한 테이블: BOOK, AUTHOR
- JOIN key: AUTHOR_ID
- 별칭: BOOK은 B, AUTHOR는 A

02.
개념 이름: INNER JOIN과 LEFT JOIN

개념 설명:
- INNER JOIN은 두 테이블에 JOIN key가 모두 존재하는 데이터만 조회한다.
- LEFT JOIN은 왼쪽 테이블의 데이터를 모두 유지하고, 오른쪽 테이블에서 일치하는 데이터를 연결한다.
- LEFT JOIN에서 오른쪽 테이블에 일치하는 데이터가 없으면 해당 컬럼에 NULL이 표시된다.
- 기준 테이블의 데이터를 모두 남겨야 할 때는 LEFT JOIN을 사용한다.

예시 쿼리:

SELECT
    O.ANIMAL_ID,
    O.NAME
FROM ANIMAL_OUTS AS O
LEFT JOIN ANIMAL_INS AS I
    ON O.ANIMAL_ID = I.ANIMAL_ID
WHERE I.ANIMAL_ID IS NULL;

- 왼쪽 테이블: ANIMAL_OUTS
- 오른쪽 테이블: ANIMAL_INS
- JOIN key: ANIMAL_ID
- ANIMAL_INS에 일치하는 기록이 없으면 I.ANIMAL_ID가 NULL이 된다.

03.
개념 이름: alias, NULL과 다중 JOIN

개념 설명:
- alias는 테이블이나 컬럼에 짧은 별칭을 붙이는 기능이다.
- JOIN을 사용할 때 별칭을 붙이면 쿼리를 짧고 명확하게 작성할 수 있다.
- NULL은 값이 0이거나 빈 문자열이라는 의미가 아니라 값이 없다는 의미이다.
- NULL을 확인할 때는 = NULL이 아니라 IS NULL 또는 IS NOT NULL을 사용한다.
- 다중 JOIN은 세 개 이상의 테이블을 차례로 연결하는 방법이다.

헷갈린 점:
- LEFT JOIN에서는 어느 테이블을 왼쪽에 작성하는지에 따라 결과가 달라질 수 있다.
- JOIN key에 중복된 값이 있으면 하나의 행이 여러 행과 연결되어 결과 행의 수가 증가할 수 있다.
- 따라서 JOIN 전후의 행 수와 JOIN key의 중복 여부를 확인해야 한다.
```

---

# 2️⃣ 수행 인증란

<img width="1512" height="735" alt="image" src="https://github.com/user-attachments/assets/3b11d9c5-9517-4653-8308-b19da7bec6ab" />


---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [조건에 맞는 도서와 저자 리스트 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/144854)

풀이 과정:

```
- 사용한 테이블: 도서 정보를 담은 BOOK 테이블과 저자 정보를 담은 AUTHOR 테이블
- JOIN key: 두 테이블에 공통으로 존재하는 AUTHOR_ID
- 날짜를 출력한 형식: DATE_FORMAT을 사용하여 %Y-%m-%d 형식으로 출력
```

<img width="804" height="735" alt="image" src="https://github.com/user-attachments/assets/054ed7bf-86de-4ab9-b523-bff6dcd151b3" />


## 🧩 문제 2

문제 링크: [상품 별 오프라인 매출 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131533)

풀이 과정:

```
- 연결한 테이블: PRODUCT 테이블과 OFFLINE_SALE 테이블
- JOIN key: PRODUCT_ID
- 집계한 값: 상품 가격과 판매량을 곱한 매출액의 합계
```

<img width="804" height="735" alt="image" src="https://github.com/user-attachments/assets/23304581-3988-445a-9f1c-3bb99a95ae0a" />


## 🧩 문제 3

문제 링크: [없어진 기록 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59042)

풀이 과정:

```
- 기준이 되는 왼쪽 테이블: 입양 기록이 저장된 ANIMAL_OUTS 테이블
- LEFT JOIN이 필요한 이유: 입양 기록은 있지만 보호소에 들어온 기록이 없는 동물도 결과에 남겨야 하기 때문
- NULL이 발생하는 경우: ANIMAL_OUTS의 동물 ID와 일치하는 기록이 ANIMAL_INS에 없는 경우
```

<img width="804" height="735" alt="image" src="https://github.com/user-attachments/assets/3f56fc32-06a7-4f5b-b51b-7a9ee98196a0" />


## 🧩 문제 4

문제 링크: [있었는데요 없었습니다](https://school.programmers.co.kr/learn/courses/30/lessons/59043)

풀이 과정:

```
- 사용한 테이블: ANIMAL_INS 테이블과 ANIMAL_OUTS 테이블
- JOIN key: ANIMAL_ID
- 비교한 날짜 컬럼: ANIMAL_OUTS의 입양일과 ANIMAL_INS의 보호 시작일
- 정렬 기준: 보호 시작일을 기준으로 오름차순 정렬
```

<img width="804" height="735" alt="image" src="https://github.com/user-attachments/assets/768ad0c7-a668-40e7-8316-6f1b21dceb2b" />


---

# 4️⃣ 참고 자료

JOIN 개념이 헷갈린다면 아래 자료를 함께 참고해도 좋습니다.

1. https://data-marketing-bk.tistory.com/entry/SQL-JOIN-%ED%95%9C-%EB%B0%A9%EC%97%90-%EC%A0%95%EB%A6%AC-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EA%B9%8C%EC%A7%80-%EC%9D%B4%EA%B2%83%EB%A7%8C-%EB%B3%B4%EC%9E%90
2. https://velog.io/@wijoonwu/JOIN

---

# 5️⃣ 이번 주 회고

```
1. INNER JOIN과 LEFT JOIN의 차이를 어떻게 이해했는지:
INNER JOIN은 두 테이블에 JOIN key가 모두 존재하는 데이터만 조회하고, LEFT JOIN은 왼쪽 테이블의 데이터를 모두 유지하는 방법으로 이해했다. 특히 LEFT JOIN에서는 오른쪽 테이블에 일치하는 데이터가 없으면 NULL이 발생하므로, 누락된 기록을 찾을 때 활용할 수 있다는 것을 알게 되었다.

2. JOIN 문제를 풀 때 가장 먼저 확인해야 할 것:
먼저 어떤 테이블의 데이터를 기준으로 조회해야 하는지 확인하고, 테이블을 연결할 수 있는 공통 컬럼인 JOIN key를 찾아야 한다. 그다음 INNER JOIN과 LEFT JOIN 중 어떤 방법이 필요한지 판단하고, JOIN key에 중복된 값이 있는지도 확인해야 한다.

3. JOIN 결과가 예상과 달랐던 경험이 있다면:
LEFT JOIN에서 왼쪽과 오른쪽 테이블의 순서를 잘못 정하면 필요한 데이터가 결과에서 빠질 수 있다는 점이 헷갈렸다. 또한 JOIN key에 중복된 값이 있으면 하나의 행이 여러 행과 연결되어 결과 행이 예상보다 많아질 수 있다는 것을 알게 되었다. 앞으로는 JOIN 전후의 행 수와 JOIN key의 중복 여부를 함께 확인하고 싶다.
```




