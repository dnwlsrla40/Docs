# FullStack Clone Project - 미정

이 프로젝트는 캠퍼스픽 - fullstack 스터디에서 자체적으로 진행한 프로젝트이며

백엔드 개발 3명
프론트 개발 3 명
데브옵스 및 형상관리 1명

위와 같이 7명이 참가한 프로젝트 입니다.

간단하게 자기소개 잠시하고 넘어가면 좋을것 같습니다.

저는 한양대학교 에리카 캠퍼스에서 전자공학을 전공하고 있는 김민수라고 합니다.  
웹개발쪽은 프론트를 주로 공부를 했구요 사용했던 프레임워크는 vue 였습니다.  
이번에 데브옵스 쪽으로 인턴을 하고 있는데 프로젝트 관리 및 풀스텍 프로젝트를  
CI/CD를 통해 관리해보는 경험을 쌓고 싶어서 이렇게 자리를 만들어 보게 되었습니다.  
앞으로 잘부탁드립니다.

[깃헙 페이지](https://github.com/Minsoo-web)

## Motivation

제각기 혼자서 개발을 진행하며 공부를 하다보니 협업의 경험도 쌓아보고 싶고,  
프로젝트를 자체적으로 설계하고 진행하면서 배워가는 것이 많을 것 같아서 이렇게 프로젝트를 기획하게 되었습니다.

프론트 엔지니어분들은 API 호출을 통한 데이터 처리에 대한 협업의 경험과  
백엔드 엔지니어분들은 CORS 이슈 및 API 배포를 통한 다양한 경험과  
데브옵스 및 프로젝트 마스터로서의 역량을 쌓아볼 수 있는 좋은 기회가 될 수 있을 것 같습니다.

추가로 제가 지난 겨울 방학때 진행하게 된 클론코딩 페이지를 잠시 소개해드리겠습니다.

[django project](http://minsoo.pythonanywhere.com/)

이정도의 완성도를 기대하고 있습니다!

## Project

이 부분을 오늘 얘기를 나누어 보고자 이렇게 다같이 모이는 자리를 마련했습니다.

우선 다같이 정해야 할 것은 다음과 같습니다.

1. 클론코딩할 서비스
2. 프론트/백 기술 스택
3. 향후 미팅 일정 계획 수립

### 클론 코딩할 서비스

우선 클론 코딩을 통해 프로젝트를 진행하게 된 경위에 대해서 말씀을 드리고 넘어가야 할 것 같습니다.

1. 디자이너의 부재
   웹 개발의 필수적인 디자인을 담당하시는 분을 섭외하기가 너무 힘들었으며  
   짧은 시간 안에 결과물을 내기에는 디자인과 병행해서 처음부터 프로젝트를 진행하기란 무리라고 생각했습니다.

2. 기획 아이디어의 부재
   죄송합니다...  
   딱히 할 말이 없네요...

3. 저작권 및 수익구조
   저희는 협업과 기술에 대한 공부를 하고자 모인 스터디이기에  
   자체적인 서비스를 통해 혹시나 상품성을 띄게 된다면 이에 상응하는 저작권 문제와 수익구조가 발생하게 될 것이며  
   이는 저와 다른 팀원들 모두 원하는 결과가 아닐 거라고 생각합니다.

이렇게 클론코딩을 통해 프로젝트를 진행하려고 했으며 클론을 하게 될 서비스 마저 제가 독단적으로 정하는 것은  
좋지 않은 판단이라고 생각해서 제가 몇가지 서비스들을 추려왔습니다.

1. Instagram

- React 기반 프로젝트
  이미 리액트로 짜여진 서비스이기 때문에 참고할 다른 문서들도 많을거라 생각하고 이미 다른 많은 분들이 클론 코딩을 통해 진행을 해온 포스팅들이 많기에 프론트 개발팀은 모르시는 게 있거나 막혔을때 참고할 문서가 많다는 점에서 좋을 것 같습니다.
- 네이티브 앱 -> 모바일 웹
  인스타그램은 아시다싶이 하이브리드 웹앱이나 모바일 웹이 아닌 리액트 네이티브로 짜여진 네이티브 앱입니다.  
   저희는 이점을 착안해서 네이티브로 짜여진 어플을 웹을 기반으로 만들었을 때의 장단점이나 네이티브 앱 개발의 필요성을 프론트 분들이 느끼시기 쉬울 것 같았습니다.
- 없는 기능이 딱히 없다.
  메신저 기능, 좋아요 및 댓글 기능, 팔로우 기능 등등 SNS 는 개발을 독학하시는 분들이 꼭 자기 힘으로 만들어 봐야 하는 많은 기능들이 있는 집약체라고 생각합니다.  
   백엔드 개발자 분들이 제일 처음 로그인 및 회원가입을 구현하고 게시판을 만들어 보듯이, 협업을 한다면 SNS 를 구현하는게 배우는게 가장 많을 것 같다고 생각했습니다.
- 과하지 않은 디자인
  다른 서비스들은 각종 라이브러리를 갖다 쓰고 싶을 만큼 화려하게 꾸며진 서비스들이 많았지만 Instagram은 심플하게 디자인이 되어 있어 프론트 개발팀이 부담이 덜할 것 같았습니다.

2. velog

- React 기반 프로젝트
  Instagram 과 같은 이유이며 추가로 velopert님 유튜브에 보면 velog를 개발하시는 과정을 라이브 코딩으로 남겨 놓으셔서 참고해서 만들어보기 편할 것 같아서 후보로 선정했습니다.
- 게시판 -> 블로그
  SNS도 배울게 엄청 많은 기능의 집약체지만 블로그도 마찬가지라고 생각합니다. 가장 기본적인 로그인, 회원가입 및 게시판을 만들어 볼 수 있는 기본중에 기본이고 처음 프로젝트를 진행하기에 부담이 가장 덜 할 것이라고 생각한 점도 후보 선정 이유중 하나입니다.

3. sta1.com

- 쇼핑몰
  velog를 블로그를 대표해서 고른 프로젝트라면 sta1.com은 유명하진 않지만 쇼핑몰 서비스를 대표할만한 기능의 집약체라고 생각합니다.
  소셜로그인, 마이페이지 구성, 검색 및 세션관리 등 배울 게 많을 거라 생각했습니다.
- 과하지 않은 디자인
  Instagram과 같은 이유로 디자인이 간단합니다. 컴포넌트 구성도 이에 따라 간단할 거라고 생각합니다.
- data_table의 구조
  어떤 db를 사용할지는 아직 미정이지만 RDBMS db를 사용한다면
  데이터 구조가 다른 서비스에 비해 간단하고 짜임새 있게 짜기 쉬울 것 같았습니다.
- vue -> react
  sta1.com은 vue의 SSR 프레임워크인 nuxt를 기반으로 제작된 서비스입니다.  
  또한 유명한 사이트가 아니다 보니 관련된 클론코딩 포스팅도 찾기 어려우며 (없었습니다.) 마주치는 모든 문제들을 직접 해결해야하는 PBL (Problem Based Learning)에 적합한 서비스라고 생각해서 골라봤습니다.

## 프론트/백엔드 기술 분석 및 선정

프론트는 리액트 개발자 분들을, 그리고 백엔드는 스프링 개발자 분들을 맞춰서 모았습니다.

이에 각자 사용하시는 추가적인 라이브러리나 기술 스택에 대해서 자유롭게 이야기 나누기 전에

각각 팀별로 팀장을 선정해야 합니다.

팀장의 역할은 크게

1. 브랜치관리 및 코드리뷰
2. 팀원별 역할 분담
3. 진행상황 milstone & github project 관리

이렇게 할당헤 드릴 예정입니다.

팀장은 우선적으로 팀내에서 합의가 끝나야 하며 무슨일이 있어도(?) 오늘안에 정해져야 합니다.
추가로 당연히 repository에 대한 push 권한을 팀장님께 드릴 예정이며 앞으로 진행되는 팀별 프로젝트 관리를 도맡아주시면 됩니다.

이제 정해주시면 됩니다!

팀장이 정해졌으면 이제 저희가 선정한 프로젝트에 쓰일 기술들과 라이브러리에 대해 자유롭게 논의 해주시면 되겠습니다.

추가로 백엔드 엔지니어분들은 spring을 쓸지 spring boot를 쓸지에 대해서도 선정해주시면 되겠습니다.

## 향후 일정 계획 수립

인원도 인원이지만 각자 사시는 곳이 너무 상이해서 저희는 앞으로

프론트 - 신도림
백엔드 - 선릉

에서 팀별로 미팅을 진행할 예정이며 팀별로 미팅을 얼마나 자주하는지에 대해는 굳이 이야기하지 않겠지만  
최소한 저와함께 프로젝트 진행 상태에 대해서 얘기를 나누고 발견된 문제점 또는 추후 계획에 대해 토의 해보는 미팅은  
일주일에 한 번은 꼭 있었으면 합니다.

그 날짜에 대해서 지금부터 정해보고 팀별로 일주일에 얼마나 만날지와 개발 시간및 프로젝트 진행 계획 수립을 정하시고  
추가적인 질의에 대해 응답하는 시간으로 마무리 짓겠습니다!