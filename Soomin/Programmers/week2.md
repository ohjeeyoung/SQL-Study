# Programmers 외
## With
### With문이란
- 이름을 가진 SubQuery를 정의한 후 사용하는 구문.
- Query의 전체적인 가독성을 높이고, 재사용할 수 있는 장점이 있음.
- 대부분의 DBMS에서 지원함.
- 계층형쿼리를 구현할 수 있음. 
- 오라클에서는 한번만 사용되면 Inline View, 두번이상 사용되면 Materialize View로 처리함.
  - 찬호샘께서 intermediate views 설명때 말씀하신 Materialize View
 
### 기본 구조
```sql
WITH [alias1] [(column1 [, column2])] as (
  SUB QUERY
)[, alias2 AS ...]
MAIN QUERY
```
- WITH [ alias ] AS ( SUB QUERY )
- 컬럼명은 생략할 수 있음.
- 쉼표(,)로 구분하여 여러개를 정의할 수 있음.
- 먼저 생성된 SubQuery는 나중에 생성하는 SubQuery에서 사용할 수 있음.
  - ex) [ alias2 ]에서 [ alias1 ]을 사용할 수 있음.
- With절 안 With 사용 가능
  - ex)
    ```sql
    WITH NEW_AND_REMOVED_WITHOUT_PROCESSING AS(
    	WITH MONTHLY_CUSTOMERS AS(
    	    SELECT ...
    	    FROM ...
    	)
    	SELECT ...
    	FROM (
    	    (
    	        SELECT ...
    	        FROM ...
    	    )
    	    UNION ALL (
    	        SELECT ...
    	        FROM ...
    	    )
    	 )NR
    	LEFT JOIN ...
    	ON ...
    )
    
    select ...
    from ...
    ```
- 단 Main Query가 없으면 실행시 에러
  
 
# Select
- Selec

## 상위 n개 레코드
