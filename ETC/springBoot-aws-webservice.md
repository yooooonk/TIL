# &#128216;[스프링부트와 AWS로 혼자 구현하는 웹서비스 - 이동욱]

## 1. spring boot 프로젝트 만들고, grealde 설정

## 2. 게시글 CRUD 화면 및 로직만들기

## 3. 구글 OAuth 설정
- __세션 값 받아오는 어노테이션 생성__
    - 'LoginUser' annotation
    - LoginUserArgumentResolver Class
        - HandlerMethodArgumentResolver 인터페이스를 구현한 클래스
        - 조건에 맞는 경우 메소드가 있다면 HandlerMethodArgumentResolver의 구현체가 지정한 값으로 해당 메소드의 파라미터로 넘길 수 있음
    - WebConfig 클래스 생성
        - LoginMvcConfigurer가 스프링에서 인식될 수 있도록 
- __세선 저장소로 데이터베이스 사용하기__
  - spring-session-jdbc 등록 : build.gradle에 의존성 등록
        compile('org.springframework.boot:spring-boot-starter-oauth2-client')
  - application.properties에 spring.session.store-type=jdbc 추가 (세선 저장소를 jdbc로 선택하도록)
- __네이버 로그인__
    - 