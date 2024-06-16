---
title: '[SpringBoot] 의존성 추천'
date: 2024-06-07 12:00:00 +0000
categories: [SpringBoot]
tags: [SpringBoot]
author: Sakua7
mermaid: true
---

<span style="color: #007bff; font-weight: bold;">본 게시물은 틀린 부분이 있을 수 있습니다, 참고 부탁드립니다. 🥹</span>

## 개발환경
* m1 mac

## SpringBoot 의존성 추천

SpringBoot를 사용하여 서버개발을 시작할때 유용한 의존성(Dependency) 정리

---

## 1. Spring Web

Spring Web은 Spring Framework에서 제공하는 모듈 중 하나로, 웹 애플리케이션을 개발하기 위한 기능을 제공합니다. 이 모듈은 전통적인 MVC 웹뿐만 아니라 RESTful 웹 서비스에도 사용되며, 개발에 필수적인 의존성입니다.

## 2. Spring Security

Spring Security는 보안을 처리하는 데 사용되는 모듈로, 사용자 인증, 권한 부여, 보안 설정 등을 관리할 수 있습니다.

## 3. MySQL, MariaDB, H2 등 사용하고자 하는 DB 드라이버

DB와의 연결을 위해 필요한 드라이버입니다.

## 3-1. Spring Data JPA

Spring Data JPA는 Hibernate와 같은 ORM을 사용하는 경우에 활용됩니다.

## 3-2. Mybatis Framework

Mybatis를 사용하는 경우에 필요한 프레임워크입니다.

## 4. Lombok

Lombok은 자바 클래스의 보일러플레이트 코드를 줄이는 데 도움을 주며, 코드의 가독성을 높일 수 있습니다.

---
