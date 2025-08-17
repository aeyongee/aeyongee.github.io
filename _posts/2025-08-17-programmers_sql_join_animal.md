---
title: 프로그래머스 문풀 - 없어진 기록 찾기
date: 2025-08-17 
categories: [Database, SQL]
tags: [SQL, 공부, 문풀, 프로그래머스]
---

프로그래머스의 SQL 고득점 Kit 중, 
**없어진 기록 찾기** 문제를 풀이하겠습니다.

카테고리: JOIN  
문제명: 없어진 기록 찾기    
레벨: 3
체감 난이도: 중간 - 알쏭달쏭


<br>

----



## 문제 설명
ANIMAL_INS 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블이다.    
ANIMAL_OUTS 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블이다.    
천재지변으로 인해 일부 데이터가 유실되었다.     
입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 ID와 이름을 ID 순으로 조회해라.    

<br>

## 문제 풀이
### 문제 요구사항 분석
1. INS - 보호소에 들어온 동물 정보, OUTS - 입양 보낸 동물 정보
2. 천재지변으로 일부 데이터가 유실됨 -> 데이터가 "없는 것"에 포커스
3. OUTS에 있는데, INS에 없는 데이터 조회
4. 동물의 ID, 이름 조회
5. ID 순 정렬


### 처음 작성한 쿼리
```sql
SELECT
    ao.ANIMAL_ID,
    ao.NAME
FROM ANIMAL_INS ai
RIGHT JOIN ANIMAL_OUTS ao
    ON ai.ANIMAL_ID = ao.ANIMAL_ID
WHERE ai.NAME IS NULL AND ao.NAME IS NOT NULL
ORDER BY
    ao.ANIMAL_ID
;
```

- 위 쿼리의 문제점
    - 누락 판정을 조인 키가 아닌 다른 칼럼으로 하려 했다.
    - 요구사항에 없는 조건이 포함되었다(OUTS 테이블의 NAME이 NULL이 아닌 경우)

<br>

### 고민의 과정
![고민의 과정](/assets/post/sql_join_animal.jpg)

<br>

### 다른 풀이 참고 + GPT가 힌트 줘서 수정한 쿼리
```sql
SELECT
    ao.ANIMAL_ID,
    ao.NAME
FROM ANIMAL_OUTS ao
LEFT JOIN ANIMAL_INS ai
    ON ao.ANIMAL_ID = ai.ANIMAL_ID
WHERE ai.ANIMAL_ID IS NULL
ORDER BY
    ao.ANIMAL_ID
;
```
- 요구사항을 요약하자면 OUTS엔 있는데, INS엔 없는 동물을 검출하는 것이다.
    - INS 테이블 레코드의 부재를 판정해야 한다.
- 레코드 부재는 칼럼 값으로 판단하면 안되고, 키 칼럼 기준으로 확인해야 한다.


<br>

### 키 포인트
> 이 문제는 부재를 검출하는 ANTI JOIN의 전형적인 패턴이다.    
> 레코드의 부재는 **조인 키 기준**으로 확인해야 한다!


<br>



<br>

## 후기
생각보다 되게 헷갈리는 문제였다. 알겠는데 모르겠는(?) 느낌이 드는 문제였다.    
결국에는 초기에 생각한 설정이 맞았지만, 부재 판정의 기준이 키 칼럼이 되어야 한다는 개념이 부족했어서 헷갈렸던 것 같다.     

항상 어떤 데이터가 있다는 가정 하에 있는 데이터를 조회하는 쿼리를 작성해왔는데,    
없다는 가정하에 어떤 데이터가 없는지를 조회하는 쿼리를 작성해보니 새롭다. 
 

