---
title: 프로그래머스 문풀 - 상품 별 오프라인 매출 구하기
date: 2025-08-17 
categories: [Database, SQL]
tags: [SQL, 공부, 문풀, 프로그래머스]
---

프로그래머스의 SQL 고득점 Kit 중, 
**상품 별 오프라인 매출 구하기** 문제를 풀이하겠습니다.

카테고리: JOIN  
문제명: 상품 별 오프라인 매출 구하기    
레벨: 2    
체감 난이도: 쉬움    


<br>

----



## 문제 설명
`PRODUCT` 테이블과 `OFFLINE_SALE` 테이블에서 상품코드 별 매출액(판매가 * 판매량) 합계를 출력하는 SQL문을 작성해라.       
결과는 매출액을 기준으로 내림차순 정렬하고 매출액이 같다면 상품코드를 기준으로 오름차순 정렬해라.    

<br>

## 문제 풀이
### 문제 요구사항 분석
1. 상품코드 별 매출액 합계 조회
2. 매출액(판매가 * 판매량)
3. 정렬은 매출액 내림차순, 상품코드 오름차순 정렬 순서대로


### 작성한 쿼리
```sql
SELECT
    p.PRODUCT_CODE,
    SUM(p.PRICE * os.SALES_AMOUNT) AS SALES
FROM PRODUCT p
JOIN OFFLINE_SALE os
    ON p.PRODUCT_ID = os.PRODUCT_ID
GROUP BY p.PRODUCT_CODE
ORDER BY
    SALES DESC,
    p.PRODUCT_CODE ASC
;
```

<br>

### 키 포인트
> 합계를 구하기 위해선 집계 함수를 사용해야 하고, 이를 위해선 `GROUP BY`를 사용해야 한다.       
> 어떤 값으로 `GROUP BY`를 사용해야 하는가? ➡️ 비교적 unique한 값!

<br>



<br>

## 후기
레벨 2여서 그런지 쉽게 풀 수 있었습니다.    

****