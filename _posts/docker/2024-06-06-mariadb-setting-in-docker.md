---
title: '[Docker] 도커에서 MariaDB 사용하기'
date: 2024-06-06 12:00:00 +0000
categories: [Docker, Mariadb]
tags: [Docker, Mariadb]
author: Sakua7
mermaid: true
---

<span style="color: #FFD700; font-weight: bold;">본 게시물은 틀린 부분이 있을 수 있습니다, 참고 부탁드립니다. 🥹</span>

## 개발환경
* m1 mac
* Docker version 24.0.2

## Mariadb In Docker

![1_pull_image](/assets/img/2024-06-06/1_pull_image.jpg)

```
docker pull mariadb
```

_docker hub에서 mariadb 이미지 pull_

---

![2_images](/assets/img/2024-06-06/2_images.jpg)

```
docker images
```

_pull 한 mariadb 이미지 생성_

---

![3_docker_run](/assets/img/2024-06-06/3_docker_run.jpg)

```
docker run --name my-mariadb -e MYSQL_ROOT_PASSWORD=myPassword -p 3306:3306 -d mariadb
```

_`docker run` : Docker container를 실행_

_`--name my-mariadb` : container 이름을 "my-mariadb"로 부여_

_`-e MYSQL_ROOT_PASSWORD=myPassword` : Mariadb의 환경변수에 password를 할당하여 root user의 비밀번호를 변경_

_`-p 3306:3306` : 호스트(외부)의 3306포트를 내부의 3306포트로 매핑하여 외부에서 Docker mariadb를 사용 가능_

_`-d mariadb` : 컨테이너를 백그라운드 모드로 실행_

---

![4_docker_ps](/assets/img/2024-06-06/4_docker_ps.jpg)

```
docker ps
```

_현재 실행 중인 Docker Container._

---

![5_docker_exec](/assets/img/2024-06-06/5_docker_exec.jpg)

```
docker exec -it (mariadb_container_name) bash
```

_Mariadb Container 내부 Bash Shell에 접속_

_bash 쉘에 진입후 SQL 쿼리 명령어를 사용_

---

![6_show_tables](/assets/img/2024-06-06/6_show_tables.jpg)

```
show databases;
```

_현재 모든 DB 목록을 표시_

_현재는 MariaDB 시스템에 관련된 DB만 있는 상태_

---

![7_create_database](/assets/img/2024-06-06/7_create_database.jpg)

```
create database (DB_name);
```

_새로운 DB를 생성_

---

![8_use_database](/assets/img/2024-06-06/8_use_database.jpg)

```
use (DB_name);
```

_해당 DB를 사용_

---

![9_create_table](/assets/img/2024-06-06/9_create_table.jpg)

```
CREATE TABLE Account (
account_id INT AUTO_INCREMENT
PRIMARY KEY,
username VARCHAR(50) NOT NULL,
email VARCHAR(100) UNIQUE NOT NULL,
password VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

_임의의 Account 테이블 생성_

---

![10_insert_data](/assets/img/2024-06-06/10_insert_data.jpg)

```
INSERT INTO Account (username, email, password)
VALUES
('john_doe', 'john@example.com', 'password123'),
('jane_smith', 'jane@example.com', 'securepwd456'),
('bob_johnson', 'bob@example.com', 'strongpass789');
```

_Account 테이블에 임의의 데이터 삽입_

---

![11_show_data](/assets/img/2024-06-06/11_show_data.jpg)

```
SELECT * FROM Account;
```

_삽입된 데이터 확인_
