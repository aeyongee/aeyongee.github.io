---
title: 프로그래머스 문풀 - 조건에 맞는 도서와 저자 리스트 출력하기
date: 2025-08-17 
categories: [Database, SQL]
tags: [SQL, 공부, 문풀, 프로그래머스]
---

프로그래머스의 SQL 고득점 Kit 중, 
**조건에 맞는 도서와 저자 리스트 출력하기** 문제를 풀이하겠습니다.

카테고리: JOIN    
문제명: 조건에 맞는 도서와 저자 리스트 출력하기     
레벨: 2    
체감 난이도: 쉬움    


<br>

----



## 문제 설명
서점의 도서정보(`BOOK`), 저자 정보(`AUTHOR`) 테이블이 있다.    
'경제' 카테고리에 속하는 도서들의 도서 ID(`BOOK_ID`), 저자명(`AUTHOR_NAME`), 출판일(`PUBLISHED_DATE`) 리스트를 출력하는 SQL문을 작성해라.    
결과는 출판일을 기준으로 오름차순 정렬해라.


<br>

## 문제 풀이
### 문제 요구사항 분석
1. '경제' 카테고리 도서 조회
2. 도서 ID, 저자명, 출판일 조회
3. 출판일 오름차순 정렬
4. 출판일은 yyyy-mm-dd 형식으로 출력(주의사항)

### 작성한 쿼리
```sql
SELECT
    b.BOOK_ID,
    a.AUTHOR_NAME,
    DATE_FORMAT(b.PUBLISHED_DATE, '%Y-%m-%d')
FROM BOOK b
JOIN AUTHOR a
    ON b.AUTHOR_ID = a.AUTHOR_ID
WHERE
    b.CATEGORY = '경제'
ORDER BY
    b.PUBLISHED_DATE ASC
;
```

<br>

### 키 포인트
> 문제 하단에 주의사항으로 출판일에 대한 출력 포맷을 정의하였다. (yyyy-mm-dd)

<br>

그대로 출판일을 출력하면, 출판일의 시-분-초도 함께 출력되기에 문제의 요구사항에 맞지 않다.    
`DATE_FORMAT` 함수를 사용하여 출판일을 yyyy-mm-dd 형식으로 출력할 수 있었다.

- `DATE_FORMAT` 사용법
    - `DATE_FORMAT(date, format)`

<br>

## 후기
레벨 2인 만큼, 쿼리 작성에 어려움이 있진 않았습니다.    
`DATE_FORMAT` 함수만 알고 있다면 쉽게 풀 수 있는 문제였는데, 저는 검색해서 함수를 사용했기에 아쉬움이 남습니다 😂

