# Backend Test 환경 구성

## 환경 설정

JDK : openJDK 13(JDK 8이하만 아니면 호환될 것입니다.)
JPA(DB) : SPA가 Database에 접근해야 하므로 Mysql도 설치하셔야 할겁니다.

## intellij 무료 버전 설치

Backend Tool인 intellij를 설치하여야 합니다. intellij는 Ultimate 버전을 사용하려면 돈을 지불해야하므로 학생 계정을 통한 무료 설치를 진행하셔야 합니다.

링크 : [intellij 무료버전 설치](https://goddaehee.tistory.com/215)

## Github 프로젝트를 intellij에 import(Clone)

intellij에 github 프로젝트를 clone하는 방법입니다.
링크 글 중 "(3)intellij를 이용한 Clone" 부분을 따라하시면 됩니다.

링크 : [intellij import](https://secuinfo.tistory.com/entry/Intellij-Github-Link)

## import 한 project 실행

src/main/resource/application.properties에 DB 접근을 위한 정보를 적어줍니다.

```
# Mysql 서버 정보
server.address=localhost
server.port=8080

# API 호출시, SQL 문을 콘솔에 출력한다.
spring.jpa.show-sql=true

# DDL 정의시 데이터베이스의 고유 기능을 사용합니다.
# ex) 테이블 생성, 삭제 등
spring.jpa.generate-ddl=true

spring.jpa.hibernate.ddl-auto=create-drop

# MySQL 을 사용할 것.
spring.jpa.database=mysql

# MySQL 설정
spring.datasource.url=jdbc:mysql://localhost:3306/db이름?useSSL=false&characterEncoding=UTF-8&serverTimezone=UTC&allowPublicKeyRetrieval=true
spring.datasource.username=mysql 계정 번호(보통 root)
spring.datasource.password=mysql 비밀번호
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

설정을 다하셨으면 아래 사진의 버튼을 눌러 서버를 열고 postman등을 이용하여 test합니다.

<img src=../../img/BE/intellij_start.JPG alt="intellij start">