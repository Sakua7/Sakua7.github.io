---
title: 'Mysql 테이블 생성'
date: 2024-06-26 12:00:00 +0000
categories: [Mysql]
tags: [Mysql]
author: Sakua7
mermaid: true
---

<span style="color: #007bff; font-weight: bold;">본 게시물은 틀린 부분이 있을 수 있습니다, 참고 부탁드립니다. 🥹</span>

# MySQL CREATE TABLE 문 구조

## 기본 구조

```sql
CREATE TABLE 테이블명 (
    열1 데이터타입 [제약조건],
    열2 데이터타입 [제약조건],
    ...
    [테이블 수준 제약조건]
);
```

### 설명

- `CREATE TABLE`: 테이블을 생성하는 SQL 명령어.
- `테이블명`: 생성할 테이블의 이름을 지정
- `열1, 열2, ...`: 테이블에 포함될 열들을 정의하고 각 열은 열 이름과 데이터 타입으로 구성
- `데이터타입`: 각 열이 저장할 데이터의 유형을 정의
- `[제약조건]`: 선택적으로 열에 적용할 제약조건을 지정할 수 있다 (예: `NOT NULL`, `UNIQUE`, `DEFAULT` 등).
- `[테이블 수준 제약조건]`: 테이블 전체에 적용할 제약조건을 지정할 수 있다 (예: `PRIMARY KEY`, `FOREIGN KEY`, `CHECK` 등).

### 예제

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    birthdate DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 설명

- `id INT AUTO_INCREMENT PRIMARY KEY`: `id` 열은 정수형 데이터 타입으로, 자동 증가 (`AUTO_INCREMENT`)되며 주 키 (`PRIMARY KEY`)로 설정
- `username VARCHAR(50) NOT NULL`: `username` 열은 최대 50자까지의 가변 길이 문자열 (`VARCHAR`)로, NULL 값이 허용되지 않는다 (`NOT NULL`).
- `email VARCHAR(100) UNIQUE`: `email` 열은 최대 100자까지의 가변 길이 문자열로, 고유한 값 (`UNIQUE`)이어야 한다.
- `birthdate DATE`: `birthdate` 열은 날짜 형식의 데이터를 저장한다.
- `created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP`: `created_at` 열은 타임스탬프 형식으로, 기본값으로 현재 시간을 설정한다 (`DEFAULT CURRENT_TIMESTAMP`).
- 
# MySQL 데이터 타입

## 숫자형 데이터

| 데이터 타입 | 설명              | 범위                                                                         | 바이트 수 |
| ----------- | ----------------- | ---------------------------------------------------------------------------- | --------- |
| TINYINT     | 정수형, 작은 범위 | -128에서 127 또는 0에서 255                                                  | 1         |
| SMALLINT    | 정수형, 작은 범위 | -32768에서 32767 또는 0에서 65535                                            | 2         |
| MEDIUMINT   | 정수형, 중간 범위 | -8388608에서 8388607 또는 0에서 16777215                                     | 3         |
| INT         | 정수형, 일반 범위 | -2147483648에서 2147483647 또는 0에서 4294967295                             | 4         |
| BIGINT      | 정수형, 큰 범위   | -9223372036854775808에서 9223372036854775807 또는 0에서 18446744073709551615 | 8         |
| FLOAT       | 부동 소수점       | -3.402823466E+38에서 3.402823466E+38                                         | 4         |
| DOUBLE      | 부동 소수점       | -1.7976931348623157E+308에서 1.7976931348623157E+308                         | 8         |
| DECIMAL     | 고정 소수점       | 사용자 지정 소수점 자릿수                                                    | 가변      |

## 날짜 및 시간형 데이터

| 데이터 타입 | 설명         | 형식                | 범위                                                |
| ----------- | ------------ | ------------------- | --------------------------------------------------- |
| DATE        | 날짜         | YYYY-MM-DD          | 1000-01-01에서 9999-12-31                           |
| TIME        | 시간         | HH:MM:SS            | -838:59:59에서 838:59:59                            |
| DATETIME    | 날짜 및 시간 | YYYY-MM-DD HH:MM:SS | 1000-01-01 00:00:00에서 9999-12-31 23:59:59         |
| TIMESTAMP   | 타임스탬프   | YYYY-MM-DD HH:MM:SS | 1970-01-01 00:00:01 UTC에서 2038-01-19 03:14:07 UTC |
| YEAR        | 연도         | YYYY                | 1901에서 2155 또는 0000                             |

## 문자열형 데이터

| 데이터 타입 | 설명                  | 최대 길이                        |
| ----------- | --------------------- | -------------------------------- |
| CHAR        | 고정 길이 문자열      | 255자                            |
| VARCHAR     | 가변 길이 문자열      | 65535자                          |
| BINARY      | 고정 길이 이진 데이터 | 255바이트                        |
| VARBINARY   | 가변 길이 이진 데이터 | 65535바이트                      |
| TINYBLOB    | 작은 이진 데이터      | 255바이트                        |
| BLOB        | 이진 데이터           | 65535바이트                      |
| MEDIUMBLOB  | 중간 크기 이진 데이터 | 16777215바이트                   |
| LONGBLOB    | 큰 이진 데이터        | 4294967295바이트                 |
| TINYTEXT    | 작은 텍스트           | 255자                            |
| TEXT        | 텍스트                | 65535자                          |
| MEDIUMTEXT  | 중간 크기 텍스트      | 16777215자                       |
| LONGTEXT    | 큰 텍스트             | 4294967295자                     |
| ENUM        | 열거형                | 미리 정의된 값 중 하나           |
| SET         | 집합형                | 미리 정의된 값 중 하나 이상의 값 |

# MySQL 열 제약조건 및 속성

## 열 제약조건

| 제약조건    | 설명                                                      |
| ----------- | --------------------------------------------------------- |
| NOT NULL    | 열 값은 NULL이 될 수 없음                                 |
| UNIQUE      | 열 값은 중복될 수 없음 (고유한 값)                        |
| PRIMARY KEY | 고유 식별자 역할을 하며, NOT NULL 및 UNIQUE 조건이 포함됨 |
| FOREIGN KEY | 다른 테이블의 열을 참조하는 외래 키 제약조건              |
| CHECK       | 특정 조건을 만족하는지 검사하는 제약조건                  |
| DEFAULT     | 기본값 설정                                               |

## 열 속성

| 속성           | 설명                                                          |
| -------------- | ------------------------------------------------------------- |
| AUTO_INCREMENT | 정수형 열에 사용하며, 자동으로 값이 증가됨                    |
| UNSIGNED       | 숫자형 열에 사용하며, 음수 값을 허용하지 않음                 |
| ZEROFILL       | 숫자형 열에 사용하며, 자릿수를 맞추기 위해 빈 자리에 0을 채움 |

## 간단한 테이블과 복잡한 테이블 생성 예시

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    hire_date DATE
);
```

```sql
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10, 2) NOT NULL CHECK (total_amount >= 0),
    status ENUM('pending', 'shipped', 'delivered', 'cancelled') NOT NULL,
    shipping_address VARCHAR(255),
    billing_address VARCHAR(255),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```