# MySQL DB Table Reference

**목차**   
[PRE](#PRE)  
[Table Reference](#Table-Reference)  
-  [User Table](#User-Table)  
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
[Table Mapping](#Table-Mapping)

## PRE

본 reference는 mysql 기준으로 작성하였습니다. 실제 Jpa에서 사용하는 Type과는 차이가 있습니다.

## Table Reference

1. **UrlSlugHistory, SeriesPost Table 삭제**

### User Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|User의 고유 id|
|username|varchar(20)|not null|User의 이름(id)|
|email|varchar(50)|UNIQUE|User가 가입할 때 사용한 email|
|velog_name|varchar(20)|default username + '.log'|User의 velog name|
|short_bio|varchar(100)||User의 한 줄 소개|
|thumbnail|Blob||User의 사진|
|profile_links|Blob||User의 소셜 정보|
|about|Text||velog 소개|

### Post Table  

1. **urlSlug, is_temp 삭제**  
2. **series_id, series_index 추가**

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|post의 고유 id|
|title|varchar(100)|not null|post 제목|
|body|Text|not null|post의 내용|
|short_description|varchar(150)|default body의 150자|post 짧은 소개|
|thumbnail|Blob||post의 썸네일 경로|
|user_id|binary(16)|FK, Index|post를 작성한 사용자에 대한 정보|
|url|varchar(100)|unique, default 고정값("/@username/") + title|post url 중복 방지(중복 시 특정 문자열 Slug를 붙임)|
|likes|Integer|default 0|좋아요 수|
|views|Integer|default 0|조회 수|
|is_private|Tinyint|default 0 Index|비공개글 check|
|released_at|TimeStamp|Index, default 작성 시간|post 등록일|
|<span style="color:red">series_id|binary(16)||post가 등록된 series 정보|
|<span style="color:red">series_index|Integer|default 0|시리즈의 post 순서를 위한 column|


### Comment Table

1. **has_reply(s), reply_to 제거**
2. **recomment, is_root, wrote_at 추가**

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|comment의 고유 id|
|post_id|binary(16)|FK, UNIQUE|comment가 달린 post id(정보)|
|user_id|binary(16)|FK, UNIQUE|comment를 단 user id(정보)|
|text|Text|not null|comment의 내용|
|level|Integer|default 0|대댓글의 갯수|
|deleted|Tinyint|default 0|comment 삭제 유무|
|<span style="color:red">recomment|binary(16)||댓글에 달린 댓글의 정보|
|<span style="color:red">is_root|Tinyint||최상위 댓글인지 check|
|<span style="color:red">worted_at|TIMESTAMP|default 작성 시간|댓글 작성일|

### Tag Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|Tag의 고유 id|
|name|varchar(50)|unique|tag 이름|

### Series Table

1. **description, url_slug 삭제**

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|Series의 고유 id|
|user_id|binary(16)|FK, UNIQUE, Index|series를 만든 user의 id(정보)|
|name|varchar(50)|not null|series 이름|
|thumbnail|Blob||series의 첫 post 썸네일 경로와 동일|
|url|varchar(100)|unique, default 고정값("/@username/series/") + seriesname
|Series url 중복 방지(중복 시 특정 문자열 Slug를 붙임)|

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

1. **post_id 삭제**
2. **user_id, tagList, url 추가**

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostHistory의 고유 id|
|title|varchar(100)|not null|임시저장할 post 제목|
|body|Text|not null|임시저장할 post의 내용|
|<span style="color:red">tag_list|Text||임시 저장글의 tag 정보|
|<span style="color:red">url|varchar(100)|unique, default id값|임시 저장글의 url|
|is_release|Tinyint|not null|작성 완료 check|
|<span style="color:red">user_id|binary(16)|Fk, UNIQUE|임시 저장글의 유저 정보|

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

1. **name column 추가**
| Key | Type | 속성 | 설명 |
|---|---|---|---|
|id|binary(16)|PK, UNIQUE|PostImage의 고유 id|
|post_id|binary(16)|FK, UNIQUE|post의 id(정보)|
|user_id|binary(16)|FK, UNIQUE|post를 작성한 user의 id(정보)|
|<span style="color:red">name|varchar(150)|not null|post에 링크된 이미지 파일 이름|
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

## Table Mapping

![DB table](../img/BE/CampusPick_Mysql_final.png)