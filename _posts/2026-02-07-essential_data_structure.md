---
title: 코딩테스트에 사용되는 필수 자료구조 모음집
date: 2026-02-07 10:30:00 
categories: [코딩테스트, 개념]
tags: [개념]
---

## 필수 자료구조
### 완전탐색(Exhaustive Search)
- 정답이 될 가능성이 있는 **모든 경우의 수**를 확인하여 정답을 찾는 알고리즘

### 배열과 List
- 데이터를 **순차적**으로 저장하는 자료구조
- 배열
    - 순차적 
    - 크기 고정
- List
    - 순차적
    - 크기 동적
    - ArrayList, LinkedListv


<br>

------

<br>

## 배열 (Array)
1. 고정된 저장 공간(fixed-size)
2. 순차적인(order) 데이터 저장
3. 메모리 연속적 할당(Contiguous)

### Random Access (Direct Access)
- n번째 index의 주소값을 산술연산 한 번으로 계산하여 즉시 접근 가능

### 단점
- 배열의 크기를 생성 시에 지정해야함, 변경 불가능

<br>

## 동적배열(Dynamic Array)
- 크기를 실행 중에 유연하게 조절할 수 있는 배열 구조
- Java : ArrayList


<br>

-----

<br>

## Linkd List
- 노드(Node)가 포인터(참조)를 통해 연결되어, 논리적 순서를 형성하는 자료구조
- 노드 객체들이 메모리상에서 연속적이지 않을 수 있지만, **참조값을 따라가면서 순서대로 데이터에 접근**함

<br>

### 단일 연결 리스트 (Singly Linked List)
- '다음(next)' 노드의 참조(주소값)만을 가짐

### 이중 연결 리스트 (Doubly Linked List)
- '다음(next)' 노드뿐만 아니라 '이전(previous)' 노드의 참조도 저장함
- 현재 노드에서 다음 노드, 이전 노드로 **양방향 탐색** 모두 가능함

### List Iterator
- Linked List의 중간의 한 지점을 계속 가리키고 싶을 때 사용함 (like cursor)


<br>

---

<br>

## Queue (큐)
- 가장 먼저 입력된 데이터가 가장 먼저 출력되는 **선입선출(FIFO)** 원칙을 따르는 자료구조
- **Enqueue**로 추가된 데이터가, **Dequeue**를 통해 가장 먼저 출력됨

<br>

### Java에서 큐 사용법
- `ArrayDeque`
  - `offer()`: enqueue
  - `poll()`: dequeue
  - `peek()` : 반환


<br>

---

<br>

## Stack (스택)
- 가장 나중에 입력된 데이터가 가장 먼저 출력되는 **후입선출(LIFO)** 원칙을 따르는 자료구조
- **Push**로 가장 최근에 추가된 데이터가 **Pop**을 통해 가장 먼저 출력됨

<br>

### Java에서 스택 사용법
- `ArrayDeque`
  - `push()`
  - `pop()`

<br>

---

<br>

## Hash table (해시테이블)
- **Key와 Value를 한 쌍으로 저장**하는 자료구조
- 해시 함수가 Key를 특정 숫자(인덱스)로 변환해주면, 데이터를 해당 위치의 배열 공간(버킷)에 바로 저장함

<br>

### Direct-address Table
- Key 값이 가리키는 위치에 바로 Value를 저장함

### Hash function
- 데이터를 **고르게 분포**하게 하는 함수가 좋은 해시 함수임

<br>

## Hash Map
> 사실상 노드를 저장하는 배열을 만드는 것임
- `put(key, value)` : 데이터 추가 (삽입 및 수정)
- `get(key)`: 데이터 조회
- `containsKey(key)` : 키 존재 여부 확인

### 순회
> HashMap은 순회할 때, 데이터를 저장한 순서(삽입 순서)를 보장하지 않음
- `entrySet()` : Key + Value 둘다 필요
- `keySet()` : Key만 필요
- `forEach()` (람다식)

<br>

---

<br>

## HashSet
- **중복된 요소를 허용하지 않는 '집합(Set)'**을 구현한 자료구조
- 내부적으로 HashMap을 활용해서 해시 원리로 데이터를 관리함
- `add(Value)` : 데이터 추가
- `remove(Value)` : 데이터 삭제
- `contains()` : 키 존재 여부 확인
    - O(1)
- `size()` : 저장된 항목 수
- 중복 데이터 추가시, `return False`

