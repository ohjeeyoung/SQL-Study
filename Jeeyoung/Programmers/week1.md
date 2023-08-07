## SELECT

- [강원도에 위치한 생산공장 목록 출력하기](#강원도에 위치한 생산공장 목록 출력하기)
- [조건에 맞는 도서 리스트 출력하기](#조건에 맞는 도서 리스트 출력하기)
- [과일로 만든 아이스크림 고르기](#과일로 만든 아이스크림 고르기)
- [평균 일일 대여 요금 구하기](#평균 일일 대여 요금 구하기)
- [인기있는 아이스크림](#인기있는 아이스크림)
- [흉부외과 또는 일반외과 의사 목록 출력하기](#흉부외과 또는 일반외과 의사 목록 출력하기)
- [3월에 태어난 여성 회원 목록 출력하기](#3월에 태어난 여성 회원 목록 출력하기)
- [12세 이하인 여자 환자 목록 출력하기](#12세 이하인 여자 환자 목록 출력하기)
- [모든 레코드 조회하기](#모든 레코드 조회하기)
- [역순 정렬하기](#역순 정렬하기)
- [아픈 동물 찾기](#아픈 동물 찾기)
- [어린 동물 찾기](#어린 동물 찾기)
- [동물의 아이디와 이름](#동물의 아이디와 이름)
- [여러 기준으로 정렬하기](#여러 기준으로 정렬하기)
- [상위 n개 레코드](#상위 n개 레코드)
- [조건에 맞는 회원수 구하기](#조건에 맞는 회원수 구하기)

----------------------------------------------------




### 강원도에 위치한 생산공장 목록 출력하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/131112

#### 코드

``` sql
SELECT FACTORY_ID, FACTORY_NAME, ADDRESS FROM FOOD_FACTORY
WHERE ADDRESS LIKE '강원도%'
ORDER BY FACTORY_ID ASC
```
----------------------------------------------------

### 조건에 맞는 도서 리스트 출력하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/144853

#### 코드

``` sql
SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE FROM BOOK
WHERE PUBLISHED_DATE LIKE '2021%' AND CATEGORY = '인문'
ORDER BY PUBLISHED_DATE ASC
```
----------------------------------------------------

### 과일로 만든 아이스크림 고르기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/133025

#### 코드

``` sql
SELECT FIRST_HALF.FLAVOR FROM FIRST_HALF, ICECREAM_INFO
WHERE FIRST_HALF.FLAVOR = ICECREAM_INFO.FLAVOR
AND FIRST_HALF.TOTAL_ORDER >= 3000 
AND ICECREAM_INFO.INGREDIENT_TYPE = 'fruit_based'
ORDER BY FIRST_HALF.TOTAL_ORDER DESC
```
----------------------------------------------------

### 평균 일일 대여 요금 구하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/151136

#### 코드

``` sql
SELECT ROUND(AVG(DAILY_FEE),0) AS AVERAGE_FEE FROM CAR_RENTAL_COMPANY_CAR
WHERE CAR_TYPE = 'SUV'
```
----------------------------------------------------


### 인기있는 아이스크림

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/133024

#### 코드

``` sql
SELECT FLAVOR FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID ASC
```

----------------------------------------------------


### 흉부외과 또는 일반외과 의사 목록 출력하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/132203

#### 코드

``` sql
SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD, '%Y-%m-%d') AS HIRE_YMD FROM DOCTOR
WHERE MCDP_CD IN ('CS', 'GS')
ORDER BY HIRE_YMD DESC, DR_NAME ASC
```

----------------------------------------------------


### 3월에 태어난 여성 회원 목록 출력하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/131120

#### 코드

``` sql
SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') FROM MEMBER_PROFILE
WHERE MONTH(DATE_OF_BIRTH) = 3 AND GENDER = 'W' AND NOT TLNO IS NULL
ORDER BY MEMBER_ID ASC
```

----------------------------------------------------


### 12세 이하인 여자 환자 목록 출력하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/132201

#### 코드

``` sql
SELECT PT_NAME, PT_NO, GEND_CD, AGE, IFNULL(TLNO, 'NONE') FROM PATIENT
WHERE AGE <= 12 AND GEND_CD = 'W'
ORDER BY AGE DESC, PT_NAME ASC
```

----------------------------------------------------


### 모든 레코드 조회하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59034

#### 코드

``` sql
SELECT * FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

----------------------------------------------------


### 역순 정렬하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59035

#### 코드

``` sql
SELECT NAME, DATETIME FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC
```

----------------------------------------------------


### 아픈 동물 찾기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59036

#### 코드

``` sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
```

----------------------------------------------------


### 어린 동물 찾기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59037

#### 코드

``` sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE INTAKE_CONDITION != 'Aged'
```

----------------------------------------------------


### 동물의 아이디와 이름

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59403

#### 코드

``` sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC
```

----------------------------------------------------


### 여러 기준으로 정렬하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59404

#### 코드

``` sql
SELECT ANIMAL_ID, NAME, DATETIME FROM ANIMAL_INS
ORDER BY NAME, DATETIME DESC
```

----------------------------------------------------


### 상위 n개 레코드

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/59405

#### 코드

``` sql
SELECT NAME FROM ANIMAL_INS
ORDER BY DATETIME ASC
LIMIT 1
```

----------------------------------------------------


### 조건에 맞는 회원수 구하기

#### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/131535

#### 코드

``` sql
SELECT COUNT(USER_ID) FROM USER_INFO
WHERE JOINED LIKE "2021%" AND AGE BETWEEN 20 AND 29
```

