## SUM, MAX, MIN / IS NULL / JOIN

- [NULL 처리하기](#NULL-처리하기)


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
