# DB Table Reference

**목차**   
[PRE](#PRE)  
[Table Reference](#Table-Reference)  
-  [Account Table](#Account-Table)  
-  [Post Table](#Post-Table)  
-  [Comment Table](#Comment-Table)  
-  [Tag Table](#Tag-Table)  

## PRE

**MongoDB의 고유 Type**

object_id : document 내에서 유일함이 보장되는 12 byte binary data  
default : 정해지지 않는 타입으로 개발자가 function등을 통해 형식을 줄 수 있습니다.  
Array(Type) : Type으로 된 배열의 형태를 가집니다.  

아직 MongoDB를 알아보고 있는 중이라 위의 내용이 Spring Boot에서 어떤 식으로 적용이 되는 지 확실하지 않습니다. 알게되는 대로 수정하겠습니다.

## Table Reference

### Account Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|_id|object_id|PK, UNIQUE|MongoDB에서 제공하는 account의 고유 id|
|account_id|String|UNIQUE|account의 id|
|password|hash|NOT_NULL|account의 password|
|posts|Array(object_id)|FK1|account가 등록한 post|
|email|String|UNIQUE|account의 Email|
|profile_image|String||account의 profile|
|nickname|String|UNIQUE|account의 nickname|
|velog_name|String|UNIQUE|개인 velog 홈페이지 name|
|temp_posts|Array(object_id)|FK2|사용자가 작성하다 그만 둔 임시 post|
|created_at|Date|default|account 등록 날짜|
|updated_at|Date|default|account 수정 날짜|
|short_intro|String||account 페이지의 한 줄 소개|
|intro|String||velog 소개|
|series|Array(String)||같은 주제의 post를 모아놓은 폴더와 같은 개념|
|read_posts|Array(object_id)|FK3|account가 읽은 post|
|is_admin|boolean||admin check|

### 추가 설명

다른 테이블과 혼동이 있을 만한 column과 velog 자체에서 제공하는 특수 기능들에 관한 추가 설명입니다.

series : velog 페이지에서 제공하는 주제가 같은 post끼리 모아놓을 수 있습니다.  
<img src=../img/series.JPG alt="series" width="500" height="300">  

profile_image : 개인 페이지의 자신의 프로필 사진입니다.  
<img src=../img/profile.JPG alt="profile_image" width="500" height="200">  

velog_name : velog 페이지의 velog 이름입니다.  
<img src=../img/velog_name.JPG alt="velog_name" width="500" height="400">  

short_intro : 개인 페이지의 한 줄 소개입니다.  
<img src=../img/short_intro.JPG alt="short_intro" width="500" height="200">  

intro : velog 페이지의 자신의 velog 소개입니다.  
<img src=../img/intro.JPG alt="intro" width="500" height="400">  

### Post Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|_id|object_id|PK, UNIQUE|MongoDB에서 제공하는 post의 고유 id|
|title|String|NOT NULL|post 제목|
|author|object_id|FK1, NOT NULL|post를 작성한 account|
|context|String|NOT NULL|post 내용|
|created_at|Date|default|post 생성 날짜|
|updated_at|Date|default|post 수정 날짜|
|deleted_at|Date|default|post 삭제 날짜|
|series|String||시리즈 명(폴더 명)|
|heart|int|default 0|좋아요 수|
|hit|int|default 0|조회 수|
|comments|Array(object_id)||post에 달린 댓글|
|tags|Array(String)|FK2|post와 관련된 tag|
|thumbnail|String||post 썸네일|
|url|String|default|account가 지정한 post의 url|
|is_private|boolean||비공개 check|
|is_completed|boolean|NOT NULL|완전히 작성된 글인지 check(임시 저장용)|

### 추가 설명

다른 테이블과 혼동이 있을 만한 column과 velog 자체에서 제공하는 특수 기능들에 관한 추가 설명입니다.

url : velog에서는 사용자가 자신의 post의 url을 지정할 수 있습니다.  
<img src=../img/url.JPG alt="profile_image" width="500" height="300">  

series : post를 등록할 때 시리즈에 포함시킬 건지 정할 수 있습니다.  
<img src=../img/post_series.JPG alt="profile_image" width="500" height="300">  

### Comment Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|_id|object_id|PK, UNIQUE|MongoDB에서 제공하는 comment의 고유 id|
|post_id|object_id|FK1, NOT NULL|comment가 달릴 post의 id|
|author|object_id|FK2, NOT NULL|comment 작성자의 account|
|comment_context|object_id|NOT NULL|comment의 내용|
|updated_at|Date|default|comment 수정 날짜|
|re_comments|Array(object_id)||comment의 comment|

### Tag Table

| Key | Type | 속성 | 설명 |
|---|---|---|---|
|_id|object_id|PK, UNIQUE|MongoDB에서 제공하는 Tag의 고유 id|
|post_id|object_id|FK NOT NULL|tag가 달릴 post의 id|
