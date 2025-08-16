---
title: JOIN 문제 풀이 (기본편)
date: 2025-08-16 23:30
categories: [Database, SQL]
tags: [SQL, 공부, 문풀]
---

이 글은 조인 관련 문제 풀이를 기록하기 위한 글입니다 😁

<br>

### 문제 1 : 주문별 상품 정보 조회
1. orders, products 테이블 INNER JOIN
2. 주문 ID, 상품명, 주문 수량 조회
3. order_in 오름차순 정렬
4. 테이블 별칭 사용

```sql
SELECT
	o.order_id,
	p.`name`,
	o.quantity
FROM orders o
JOIN products p
ON o.product_id = p.product_id
ORDER BY o.order_id;
```

<br>

### 문제 2 : 3개 테이블 조인
1. orders, users, products 테이블 모두 조인
2. SHIPPED 상태인 주문 조회
3. 주문 ID, 고객 이름, 상품명, 주문 날짜 조회

```sql
SELECT
	o.order_id,
	u.`name` as user_name,
	p.`name` as product_name,
	o.order_date
FROM 
	orders o
JOIN 
	users u ON o.user_id = u.user_id
JOIN 
	products p ON o.product_id = p.product_id
WHERE 
	o.status = 'SHIPPED';
```

<br>

### 문제 3 : 고객별로 총 구매액 계산하기
1. INNER JOIN, 집계 함수 사용하여 각 고객이 지금까지 주문한 총 구매액 계산
2. 고객 이름(user_name), 총 구매액(total_purchase_amount) 조회
3. 총 구매액이 높은 순서대로 정렬 (총 구매액 = 주문수량 * 상품가격)

<br>

이 문제는 풀이하다가 중간에 막힌 부분이 있었다.
- 내가 작성한 쿼리
```sql
SELECT
	users.`name` AS user_name,
	orders.quantity * products.price AS total_purchase_amount
FROM orders
JOIN
	users ON orders.user_id = users.user_id
JOIN 
	products ON orders.product_id = products.product_id
ORDER BY total_purchase_amount DESC;
```

<br>


- 정답을 참고해서 수정한 쿼리
```sql
SELECT
	u.`name` AS user_name,
	SUM(o.quantity * p.price) AS total_purchase_amount
FROM orders o
JOIN
	users u ON o.user_id = u.user_id
JOIN 
	products p ON o.product_id = p.product_id
GROUP BY
	u.`name`
ORDER BY total_purchase_amount DESC;
```

- 집계함수를 사용하기 위해선 `GROUP BY`를 사용해야 한다는 것을 알 수 있었다.

<br>

### 문제 4 : 특정 카테고리의 미판매 상품 찾기
1. products, orders 테이블 LEFT JOIN
2. '전자기기' 카테고리 포함 제품 조회
3. 그중 판매된적 없는 상품 조회
4. 상품의 이름과 가격 조회

```sql
SELECT
	p.`name`,
	p.price
FROM 
	products p 
LEFT JOIN 
	orders o ON p.product_id = o.product_id
WHERE 
	p.category = '전자기기' AND o.order_id IS NULL
;
```

<br>

### 문제 5 : 고객별 주문 횟수 구하기 (주문 없는 고객 포함)
1. 모든 고객의 이름과 각 고객이 주문한 총 횟수를 조회
2. 주문을 하지 않은 고객은 주문 횟수가 0으로 표시
3. 정렬은 고객 이름 오름차순

```sql
SELECT
	u.`name` AS name,
	COUNT(o.order_id) AS order_count
FROM users u 
LEFT JOIN
	orders o ON o.user_id = u.user_id
GROUP BY 
	name
ORDER BY
	name;
```

<br>

### 문제 6 : RIGHT JOIN으로 주문 없는 고객 찾기
1. RIGHT JOIN 사용하기
2. 가입은 했지만, 주문 이력이 없는 고객 조회
3. 고객의 이름과 이메일 조회

```sql
SELECT
	u.`name`,
	u.email
FROM orders o 
RIGHT JOIN 
	users u ON o.user_id = u.user_id
WHERE
	o.order_id IS NULL 
;
```

<br>

### 문제 7 : 고객별 주문 상품 목록 조회하기
1. 모든 고객의 이름, 그 고객이 주문한 상품의 이름 조회
2. 여러 상품을 구매했으면, 모든 상품명을 조회
3. 주문 기록이 없다면, 상품명 NULL 
4. 정렬은 고객 이름, 상품 이름 순

```sql
SELECT 
	u.`name` AS user_name,  
	p.`name` AS product_name
FROM users u 
LEFT JOIN 
	orders o ON u.user_id = o.user_id
LEFT JOIN 
	products p ON o.product_id = p.product_id
ORDER BY 
	user_name, product_name
;
```

<br>

### 문제 8 : 특정 상사의 부하 직원 찾기
1. employees 테이블 셀프 조인
2. 최과장의 직속 부하 직원 조회
3. 이름, 직원 ID 조회

```sql
SELECT
	e2.employee_id,
	e2.`name` ,
	e2.manager_id,
	e1.`name` AS manager_name
FROM employees e1 
JOIN 
	employees e2 ON e1.employee_id = e2.manager_id
WHERE 
	e1.`name` = '최과장';
```

<br>

### 문제 9 : 모든 상품 옵션 조합에 재질 추가하기
1. materials 테이블 새로 만들기 (면, 실크 옵션 존재)
2. sizes, colors 테이블 CROSS JOIN
3. materials 테이블 생성 후 데이터 삽입
4. sizes, colors, materials 테이블 CROSS JOIN 
5. CONCAT 함수로 상품명-색상-사이즈-재질 형식으로 product_full_name 생성

```sql
CREATE TABLE `materials` (
	material VARCHAR(40) PRIMARY KEY
);

INSERT `materials` 
VALUES 
	('Cotton'),
	('Silk')
;


SELECT 
	CONCAT('기본티셔츠', '-', c.color, '-', s.`size`, '-', material) AS product_full_name,
	s.`size`,
	c.`color`,
	m.`material`
FROM sizes s 
CROSS JOIN 
	colors c
CROSS JOIN 
	materials m
;
```

<br>

### 문제 10 : 특정 고객의 주문 내역 상세 조회하기
1. users, orders, products 3개의 테이블 조인
2. 모든 상품 이름(product_name), 주문 날짜(order_date), 주문 수량(quantity) 조회
3. 주문 날짜 최신순 정렬(내림차순)

```sql
SELECT 
	u.`name` AS customer_name,
	p.`name` AS product_name,
	o.order_date,
	o.quantity
FROM orders o  
JOIN
	users u ON o.user_id = u.user_id
JOIN 
	products p ON o.product_id = p.product_id
WHERE 
	u.`name` = '네이트'
ORDER BY 
	o.order_date DESC
;
```

<br>

### 문제 11 : 서울 지역 고객의 총 주문 금액 계산하기
1. JOIN과 집계 함수 사용
2. users, orders, products 테이블 조인
3. '서울'에 거주하는 고객별로 총 주문 금액(total_spent) 계산
4. 총 주문 금액은 각 주문의 가격(price) * 수량(quantity) 합계
5. 총 주문 금액이 높은 순 정렬 (내림차순)

```sql
SELECT 
	u.`name` AS customer_name,
	SUM(p.price * o.quantity) AS total_spent
FROM orders o 
JOIN 
	users u ON o.user_id = u.user_id
JOIN
	products p ON o.product_id = p.product_id
WHERE 
	u.address LIKE '서울%'
GROUP BY u.user_id
ORDER BY 
	total_spent DESC
;
```