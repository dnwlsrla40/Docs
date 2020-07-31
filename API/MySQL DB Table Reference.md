# MySQL DB Table Reference

**목차**   
[PRE](#PRE)  
[Table Reference](#Table-Reference)  
-  [Account Table](#Account-Table)  
-  [Post Table](#Post-Table)  
-  [Comment Table](#Comment-Table)  
-  [Tag Table](#Tag-Table)  
-  [Series Table](#Series-Table)  
-  [PostTag Table](#PostTag-Table)  
-  [PostLike Table](#PostLike-Table)  
-  [PostHistory Table](#PostHistory-Table) 
-  [PostRead Table](#PostRead-Table) 
-  [PostScore Table](#PostScore-Table) 
-  [PostImage Table](#PostImage-Table) 
-  [SeriesPost Table](#SeriesPost-Table)
-  [UrlSlugHistory Table](#UrlSlugHistory-Table)   

## PRE

본 reference는 mysql 기준으로 작성하였습니다. 실제 Jpa에서 사용하는 Type과는 차이가 있습니다.

**MongoDB의 고유 Type**


## Table Reference

### User Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|User의 고유 id|
|username|varchar(20)|not null|User의 이름(nickname)|
|password|varchar(32)||User의 password|
|email|varchar(50)|UNIQUE|User가 가입할 때 사용한 email|
|display_name|varchar(20)|default username + '.log'|User의 velog name|
|short_bio|varchar(100)||User의 한 줄 소개|
|thumbnail|Blob||User의 사진|
|profile_links|Blob||User의 소셜 정보|
|about|Text||velog 소개|
|salt|varchar(4)||비밀번호 암호화를 위한 column|

### Post Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|post의 고유 id|
|title|varchar(100)|not null|post 제목|
|body|Text|not null|post의 내용|
|short_description|varchar(150)||post 짧은 소개|
|thumbnail|Blob||post의 썸네일|
|user_id|binary(16)|FK, Index|post를 작성한 사용자에 대한 정보|
|url_slug|varchar(100)||post url 중복 방지|
|likes|Integer|default 0|좋아요 수|
|views|Integer|default 0|조회 수|
|is_temp|Tinyint|default 1 Index|임시저장글 check|
|is_private|Tinyint|default 0 Index|비공개글 check|
|released_at|TimeStamp|Index|post 등록일|

### Comment Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|comment의 고유 id|
|post_id|binary(16)|FK, UNIQUE|comment가 달린 post id(정보)|
|user_id|binary(16)|FK, UNIQUE|comment를 단 user id(정보)|
|text|Text|not null|comment의 내용|
|reply_to|binary(16)||comment의 comment|
|level|Integer|default 0|대댓글의 갯수|
|has_replies|Tinyint||대댓글 유무|
|deleted|Tinyint||comment 삭제 유무|

### Tag Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|Tag의 고유 id|
|name|varchar(50)||tag 이름|

### Series Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|Series의 고유 id|
|user_id|binary(16)|FK, UNIQUE, Index|series를 만든 user의 id(정보)|
|name|varchar(50)|not null|series 이름|
|description|Text||series 설명|
|thumbnail|Blob||series 사진|
|url_slug|varchar(100)||Series url 중복 방지|

### PostTag Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostTag의 고유 id|
|post_id|binary(16)|FK, UNIQUE|tag가 달린 post의 id(정보)|
|tag_id|binary(16)|FK, UNIQUE|post에 달린 tag의 id(정보)|

### PostLike Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostLike의 고유 id|
|post_id|binary(16)|FK, UNIQUE|좋아요 눌린 post의 id(정보)|
|user_id|binary(16)|FK, UNIQUE|좋아요 누른 user의 id(정보)|

### PostHistory Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostHistory의 고유 id|
|post_id|binary(16)|FK, UNIQUE| 임시저장될 post의 id(정보)|
|title|varchar(100)|not null|임시저장할 post 제목|
|body|Text|not null|임시저장할 post의 내용|
|is_release|Tinyint|not null|작성 완료 check|

### PostRead Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostRead의 고유 id|
|post_id|binary(16)|FK, UNIQUE|읽힌 post의 id(정보)|
|user_id|binary(16)|FK, UNIQUE|post를 읽은 user의 id(정보)|

### PostScore Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostScore의 고유 id|
|post_id|binary(16)|FK, UNIQUE|트렌딩 페이지에 올라갈 post의 id(정보)|
|user_id|binary(16)|FK, UNIQUE|트렌딩 페이지에 올라갈 post를 작성한 user의 id(정보)|
|type|varchar()||아직 모르겠습니다.|
|score|Float|default 0|post의 순위를 메길 점수(예상: 조회수, 좋아요수, 댓글수, 등록일)|

### PostImage Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostImage의 고유 id|
|post_id|binary(16)|FK, UNIQUE|post의 id(정보)|
|user_id|binary(16)|FK, UNIQUE|post를 작성한 user의 id(정보)|
|path|Blob|not null|post에 링크된 이미지 경로|
|file_size|Integer||이미지 파일의 크기|

### SeriesPost Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|SeriesPost의 고유 id|
|series_id|binary(16)|FK, UNIQUE|series의 id(정보)|
|post_id|binary(16)|FK, UNIQUE|series에 포함된 post의 id(정보)|
|index|Integer||series의 post 순서(정렬)을 위해 사용하는 column|

### UrlSlugHistory Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|UrlSlugHistory의 고유 id|
|post_id|binary(16)|FK, UNIQUE|post의 id(정보)|
|user_id|binary(16)|FK, UNIQUE|user의 id(정보)|
|url_slug|varchar(100)|||