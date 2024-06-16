---
title: '[Docker] Mariadb에 dummy db 삽입하기'
date: 2024-06-16 00:00:00 +0000
categories: [Docker, Mariadb]
tags: [Docker, Mariadb]
author: Sakua7
mermaid: true
---

<span style="color: #007bff; font-weight: bold;">본 게시물은 틀린 부분이 있을 수 있습니다, 참고 부탁드립니다. 🥹</span>

## 개발환경
* m1 mac
* Docker version 24.0.2

**본 게시물은 docker에서 mariadb가 실행 중임을 가정합니다, docker에 mariadb를 올리는 방법은 다음 게시물에서 확인할 수 있습니다.**

<div style="background-color: #007bff; padding: 10px; border-radius: 15px; text-align: center;">
    <a href="https://sakua7.github.io/posts/mariadb-setting-in-docker/" style="color: white;  font-size: 1.2em;">
        [Docker] 도커에서 MariaDB 사용하기
    </a>
</div>

--- 
위 게시물에서 docker에서 mariadb를 올렸다면 이제 dummy db를 추가하는 방법을 알아보자.

다음 링크를 들어가면 여러가지 dummy db를 다운받을수 있는데 본 게시물에서는 world.sql을 사용해보려한다
<div style="background-color: #007bff; padding: 10px; border-radius: 15px; text-align: center;">
    <a href="https://sakua7.github.io/posts/mariadb-setting-in-docker/" style="color: white;  font-size: 1.2em;">
        https://dev.mysql.com/doc/index-other.html
    </a>
</div>

![dummy_db_1](/assets/img/2024-06-16/dummy_db_1.png)
![dummy_db_2](/assets/img/2024-06-16/dummy_db_2.png)
**world database의 Zip 형태로 받아주고 압축을 풀면 world.sql 파일이 생성된다.**

---

world.sql 파일이 있는 위치에서 docker로 파일을 복사해 준다.
![dummy_db_3](/assets/img/2024-06-16/dummy_db_3.png)
```
docker cp world.sql (containerName):/world.sql
```

---

docker container 내부에서 mariadb에 sql 파일을 가져온다.
![dummy_db_4](/assets/img/2024-06-16/dummy_db_4.png)

```
docker exec -it (conainterName) mariadb -uroot -p -e "source /world.sql"
```

---

db에 접속해 보면 world 추가되고 여러 테이블을 확인할 수 있다.
![dummy_db_5](/assets/img/2024-06-16/dummy_db_5.png)
![dummy_db_6](/assets/img/2024-06-16/dummy_db_6.png)

---

쿼리문들을 작성하여 연습할 수 있다.
![dummy_db_7](/assets/img/2024-06-16/dummy_db_7.png)
