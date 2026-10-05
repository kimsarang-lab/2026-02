<img width="1031" height="871" alt="image" src="https://github.com/user-attachments/assets/c3028615-6660-4430-b5a0-f00686e9e0f4" />﻿# 📘 SQL_BASIC 5주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 날짜/시간 데이터와 조건문을 학습합니다. 특히 `CASE WHEN`은 SQL 문제 풀이와 데이터 분석에서 자주 사용되므로, 직접 분류 기준을 만들고 결과를 확인하는 연습을 해주세요.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_5th_TIL

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기

### 4-6. 조건문(CASE WHEN, IF)

---

## ✨ 선택 강의

- 4-5. 시간 데이터 연습문제: 날짜/시간 함수를 더 연습하고 싶을 때 선택 수강
- 4-7. 조건문 연습문제: CASE WHEN과 IF를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | ✅ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | ✅ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | ✅ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | 🍽️ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념 정리

아래 키워드 중 중요하다고 생각한 개념을 2개 이상 골라 짧게 정리해주세요. 3개보다 더 많이 정리하고 싶다면 자유롭게 항목을 추가해도 좋습니다.

이번 주 키워드:
- DATE
- DATETIME
- TIMESTAMP
- EXTRACT
- DATETIME_TRUNC
- FORMAT_DATETIME
- CASE WHEN
- IF

## 01.

```
개념 이름:
개념 설명:
예시 쿼리:
```

## 02.

```
개념 이름:
개념 설명:
예시 쿼리:
```

## (선택) 03.

```
개념 이름:
개념 설명:
헷갈린 점:
```

---

# 2️⃣ 수행 인증란

<img width="399" height="412" alt="image" src="https://github.com/user-attachments/assets/57cf23ea-4ae1-499f-9ec4-4a83bf07983a" />


---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [자동차 대여 기록에서 장기/단기 대여 구분하기](https://school.programmers.co.kr/learn/courses/30/lessons/151138)

풀이 과정:

```
- 장기/단기 대여를 나눈 기준:
대여 시작일과 종료일을 모두 포함한 대여 기간이 30일 이상이면 '장기 대여', 30일 미만이면 '단기 대여'로 분류하였다.

- 사용한 날짜 계산 방식:
DATEDIFF(END_DATE, START_DATE)를 사용하여 두 날짜의 차이를 계산하였다. 시작일과 종료일을 모두 대여 기간에 포함하기 위해 계산 결과에 1을 더하였다.

- CASE WHEN으로 만든 컬럼:
대여 기간이 30일 이상인지 확인하여 '장기 대여' 또는 '단기 대여'를 표시하는 RENT_TYPE 컬럼을 만들었다.
```

<img width="1031" height="871" alt="image" src="https://github.com/user-attachments/assets/f7a8b2ef-7aa0-4891-aacc-d393ddad08ea" />
>

## 🧩 문제 2

문제 링크: [한 해에 잡은 물고기 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298516)

풀이 과정:

```
- 문제에서 요구한 연도:
2021년에 잡은 물고기의 수를 구해야 한다.

- 사용한 날짜 조건:
YEAR(TIME)을 사용하여 물고기를 잡은 날짜에서 연도를 추출하고, 그 값이 2021인 기록만 선택하였다.

- 집계한 대상:
2021년에 잡은 물고기 기록의 전체 행 수를 COUNT(*)로 계산하고, 결과 컬럼의 이름을 FISH_COUNT로 지정하였다.
```

<img width="1031" height="871" alt="image" src="https://github.com/user-attachments/assets/aa9a885c-f914-480f-8050-aff06aeb493e" />


## 🧩 문제 3

문제 링크: [조건에 부합하는 중고거래 상태 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/164672)

풀이 과정:

```
- 날짜 조건:
2022년 10월 5일에 등록된 게시물만 조회하기 위해 WHERE CREATED_DATE = '2022-10-05'를 사용하였다.

- CASE WHEN으로 바꾼 값:
STATUS가 SALE이면 '판매중', RESERVED이면 '예약중', DONE이면 '거래완료'로 변경하였다.

- ELSE에 해당하는 경우:
SALE, RESERVED, DONE 중 어느 조건에도 해당하지 않으면 기존의 STATUS 값을 그대로 반환하도록 작성하였다.

- 정렬 기준:
게시글 ID를 기준으로 내림차순 정렬하기 위해 ORDER BY BOARD_ID DESC를 사용하였다.
```

<img width="1031" height="871" alt="image" src="https://github.com/user-attachments/assets/1dbd2f4e-11cc-4639-8c56-7ab700dfca27" />


## 🧩 문제 4

문제 링크: [자동차 평균 대여 기간 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157342)

풀이 과정:

```
- GROUP BY 기준:
자동차별 평균 대여 기간을 계산하기 위해 CAR_ID를 기준으로 그룹화하였다.

- 평균을 계산한 방식:
각 대여 기록의 대여 기간을 DATEDIFF(END_DATE, START_DATE) + 1로 계산한 후, AVG를 사용하여 자동차별 평균 대여 기간을 계산하였다. ROUND를 사용하여 소수점 둘째 자리에서 반올림하고 소수점 첫째 자리까지 표시하였다.

- HAVING에 사용한 조건:
자동차별 평균 대여 기간을 계산한 후, 평균 대여 기간이 7일 이상인 자동차만 조회하기 위해 HAVING AVG(DATEDIFF(END_DATE, START_DATE) + 1) >= 7을 사용하였다.

- 처음 헷갈렸던 점:
개별 대여 기록에 조건을 적용하는 것이 아니라 자동차별 평균을 구한 후 조건을 적용해야 하므로 WHERE가 아니라 HAVING을 사용해야 한다는 점이 헷갈렸다.
```

<img width="1031" height="871" alt="image" src="https://github.com/user-attachments/assets/f6a320d3-2851-4a54-b68c-33dfcb4ddb98" />


---

# 4️⃣ 이번 주 회고

```
1. 날짜 함수 중 가장 헷갈린 함수:
DATEDIFF가 가장 헷갈렸다. 두 날짜의 차이를 계산할 때 시작일은 포함되지 않기 때문에, 시작일과 종료일을 모두 포함한 실제 이용 기간을 구하려면 계산 결과에 1을 더해야 한다는 점을 기억해야겠다.

2. CASE WHEN을 사용할 때 기억해야 할 문법:
WHEN 뒤에는 조건을 작성하고 THEN 뒤에는 조건을 만족할 때 반환할 값을 작성해야 한다. 여러 조건을 순서대로 작성할 수 있으며, 어떤 조건에도 해당하지 않는 경우는 ELSE로 처리한다. 마지막에는 반드시 END를 작성해야 한다.

3. 날짜/시간 데이터나 조건문을 활용해보고 싶은 분석 상황:
연구 데이터에서 입원일과 퇴원일을 이용해 재원 기간을 계산하거나, 퇴원 후 재입원까지 걸린 기간을 구할 때 날짜 함수를 활용해보고 싶다. 또한 연령, 재원 기간, 재입원 시점 등을 일정한 기준에 따라 집단으로 분류할 때 CASE WHEN을 사용해보고 싶다.
```

수고하셨습니다!




