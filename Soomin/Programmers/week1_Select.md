# Select
- Select를 하는 주 이지만 여러 종류의 문제가 뒤섞여서 나오는 바람에 의도치않게 다양하게 풀어버렸다...
- 따라서 아래 문제들이 select 문제가 아닐 수 있음

## 상위 n개 레코드
- MySQL에서는 select에서 사용할 수 있는 Top 함수가 없으므로, limit을 사용한다
  ```sql
  SELECT NAME
  FROM ANIMAL_INS
  ORDER BY DATETIME
  LIMIT 1
  ```


## 날짜 필터링
- LIKE
  - 날짜로 필터링할 때 LIKE 연산자를 사용하는 것은 성능상 좋지 않은 방법임.
  - LIKE 연산자는 문자열 비교를 위해 사용되며, 날짜와 시간을 비교하는데 적합하지 않기 때문에 성능이 저하될 수 있음
  - 날짜 비교를 위해 LIKE 연산자를 사용하는 경우, 데이터베이스 엔진은 문자열로 표현된 날짜를 파싱하고 변환해야 함. -> 비효율적

- 날짜 함수
  - 대부분의 데이터베이스 시스템은 날짜와 시간을 처리하기 위한 특정 함수들을 제공.
  - 예를 들어, MySQL에서는 DATE() 함수를 사용하여 날짜를 추출하거나 BETWEEN 연산자를 사용하여 범위를 지정하는 등의 방법을 사용할 수 있음.
  - 올바른 방법은 데이터베이스 시스템에 맞는 날짜 및 시간 함수를 사용하여 날짜를 필터링하고 비교하는 것. -> 데이터베이스 시스템이 내부적으로 최적화하여 효율적으로 처리할 수 있으며, 성능 저하를 최소화할 수 있음


## 최댓값 가진 행 전체 정보 출력
- Where절에 Max함수 사용했더니 에러
  ```sql
  SELECT PRODUCT_ID, PRODUCT_NAME, PRODUCT_CD, CATEGORY, PRICE
  FROM FOOD_PRODUCT
  WHERE PRICE = MAX(PRICE)
  ```
  -> Group function 잘못 사용

- 서브쿼리의 Select절에서 사용할 것
  ```sql
  SELECT PRODUCT_ID, PRODUCT_NAME, PRODUCT_CD, CATEGORY, PRICE
  FROM FOOD_PRODUCT
  WHERE PRICE = (SELECT MAX(PRICE) FROM FOOD_PRODUCT)
  LIMIT 1
  ```

## Union (오프라인/온라인 판매 데이터 통합하기 - Level 4)
- join 후 오프라인/온라인 판매량을 합치는 것인줄 알았으나 Union 후 단순 출력하는 것이었음
  ```sql
  SELECT DATE_FORMAT(SALES_DATE, '%Y-%m-%d') AS SALES_DATE,
    PRODUCT_ID,
    USER_ID,
    SALES_AMOUNT
  FROM ONLINE_SALE
  WHERE SALES_DATE >= '2022-03-01' AND SALES_DATE < '2022-04-01'
  
  UNION ALL
  
  SELECT DATE_FORMAT(SALES_DATE, '%Y-%m-%d') AS SALES_DATE,
      PRODUCT_ID,
      NULL AS USER_ID,
      SALES_AMOUNT
  FROM OFFLINE_SALE
  WHERE SALES_DATE >= '2022-03-01' AND SALES_DATE < '2022-04-01'
  
  ORDER BY SALES_DATE, PRODUCT_ID, USER_ID
  ```
  
# GROUP BY
## SET (입양 시각 구하기 2 - Level 4)
- 단순히 Groupby 해버리면 입양이 발생하지 않은 시간대는 출력되지 않음
  ```sql
  SELECT HOUR(DATETIME) AS HOUR, COUNT(*) AS COUNT
  FROM ANIMAL_OUTS
  GROUP BY HOUR(DATETIME)
  ORDER BY HOUR
  ```
  
- 데이터가 없는 시간대를 위해 set 사용
  ```sql
  SET @HOUR = -1;
  SELECT (@HOUR := @HOUR +1) AS HOUR,
      (SELECT COUNT(HOUR(DATETIME)) 
      FROM ANIMAL_OUTS 
      WHERE HOUR(DATETIME)=@HOUR) AS COUNT 
      FROM ANIMAL_OUTS
  WHERE @HOUR < 23;
  ```
  - SET은 어떤 변수에 특정 값 할당할 떄 쓰는 명령어
  - SET @hour := -1 : 사용자 지정 변수 hour을 선언, 변수 값은 -1 (0시부터 나타내야함, 1씩 증가할거라)
  - @hour := @hour + 1 : ROW가 한번 지날 때마다 +1 (1씩 시간대가 증가)
  - WHERE @hour < 23 : 24시까지만 나타내고 종료
