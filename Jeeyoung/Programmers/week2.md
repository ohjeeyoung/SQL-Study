## SUM, MAX, MIN / IS NULL / JOIN

- [NULL 처리하기](#NULL-처리하기)
- [조건에 맞는 사용자와 총 거래금액 조회하기](#조건에-맞는-사용자와-총-거래금액-조회하기)
- [자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기](#자동차-대여-기록에서-대여중-/-대여-가능-여부-구분하기)

----------------------------------------------------

## IS NULL
### NULL 처리하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59410

#### 코드

``` sql
SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') AS NAME, SEX_UPON_INTAKE 
FROM ANIMAL_INS
```

IFNULL

----------------------------------------------------
## JOIN
### 조건에 맞는 사용자와 총 거래금액 조회하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/164668

#### 코드

``` sql
SELECT B.USER_ID, B.NICKNAME, SUM(PRICE) AS TOTAL_SALES
FROM USED_GOODS_BOARD AS A, USED_GOODS_USER AS B
WHERE A.WRITER_ID = B.USER_ID AND A.STATUS = 'DONE'
GROUP BY B.USER_ID
HAVING SUM(PRICE) >= 700000
ORDER BY 3 ASC
```
WHERE과 HAVING의 차이


----------------------------------------------------


### 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/157340

#### 코드

``` sql
SELECT CAR_ID, CASE WHEN '2022-10-16' BETWEEN start_date AND end_date 
                THEN '대여중'
                ELSE '대여 가능' END AS AVAILABILITY
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE end_date >= '2022-10-16'
GROUP BY 1
ORDER BY 1 DESC
```

CASE 


----------------------------------------------------
