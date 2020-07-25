# Vue.js란
- MVVM 패턴의 ViewModel 레이어에 해당하는 화면단 라이브러리
### MVVM 패턴이란?
- View <-> ViewModel <-> Model
- Backend 로직과 Client의 마크업 & 데이터 표현단을 분리하기 위한 구조로 전통적인 MVC 패턴의 방식에서 기인
- 화면 앞단의 화면 동작 관련 고직과 뒷단의 DB 데이터 처리 및 서버 로직을 분리하고, 뒷단에서 넘어온 데이터를 Model에 담아 View로 넘겨주는 중간 지점  
### MVC 패턴과의 차이?
- MVC 패턴 
    - Model : 프로그램에서 사용하는 실제 데이터 및 데이터 조작 로직을 처리하는 부분
    - View : 사용자에게 제공되어 뵤여지는 UI 부분
    - Controller : 사용자의 입력을 받고 처리하는 부분
    - 뷰와 모델이 의존적이라는 단점
- MVP 패턴
    - Model + View + Presenter
    - Presenter : View에서 요청한 정보를 Model로 부터 가공해서 View로 전달하는 부분    
    - 사용자 입력을 MVC와 달리 View에서 받음
    - View로 사용자 입력이 들어옴 -> View는 Presenter에 작업 요청을 함 -> Presenter에서 필요한 데이터를 Model에 요청 ->Model은 Presenter에 필요한 데이터를 응답 ->Presenter는 View에 데이터를 응답 -> View는 Presenter로부터 받은 데이터로 화면에 보여줌
    - View와 Model의 의존성은 없지만 View와 Presenter가 1:1로 강한 의존성을 가짐
- MVVM 패턴
    - View + ViewModel + Model
    - ViewModel : View를 표현하기 위해 만들어진 View를 위한 Model
    - Command패턴과 Data Binding 패턴을 사용해 View와 ViewModel의 의존성이 사라짐
    - View에서 입력이 들어오면 Command 패턴을 통해 ViewModel에 명령을 내리게 되고 Data Binding으로 인해 ViewModel의 값이 변화하면 바로 View의 정보가 바뀐다
    - View에 입력이 들어오면 Command 패턴으로 ViewModel에 명령-> ViewModel은 필요한 데이터를 Model에 요청 -> Model은 ViewModel에 필요한 데이터를 응답 ->ViewModel은 응답 받은 데이터를 가공해서 저장 -> View는 ViewModel과의 Data Binding으로 인해 자동갱신
# PWA(Progressive web applications)
- native app와 웹의 장점을 결합해 만듦
- 웹 소프트웨어의 일종으로 HTML,CSS,자바스크립트를 포함한 웹 기술들을 사용해 만듦
- 표준을 준수하는 브라우저를 사용하는 어떠한 플랫폼에서도 동작하도록 고안됨
- 오프라인 작업, 푸시 알림, 장치 하드웨어 접근, 데스크톱과 모바일 장치의 네이티브 애플리케이션과 유사한 사용자 경험을 제공 ->Native 기능을 지원
- 웹 애플리케이션이기 때문에 개발자나 사용자가 앱 스토어를 통해 설치할 필요가 없음

# SPA(Single Page Application)
- 서버로부터 완전한 새로운 페이지를 불러오지 않고 현재의 페이지를 동적으로 다시 작성

# Component
- Vue.js는 기본적으로 화면 또는 기능을 적절하게 분리하여 컴포넌트화 시켜서 개발을 하고 이것을 연결하여 프로그램이 작동하도록 구현하는 방법을 사용한다

# SFC(Single File Component)
- 페이지내 Script 선언 방식의 약점
    - 모든 컴포넌트에 대한 고유한 이름 필요
    - String 구문 강조가 약함, 여러 줄로 HTML에 보기 안좋은 슬래시
    - CSS가 모듈화되지 않음
    - 전처리기가 아닌 HTML 및 ES6 JavaScript로 제한(ES6 지원 x)

- 화면의 특정 영역에 대한 HTML, JS, CSS 코드를 한 파일 안에서 관리하는 방법
- -.vue 확장자를 가진 모든 파일
- _뷰 로더_ 에 의해 HTML, CSS, JS와 같은 웹 자원으로 분리되어 실행됨
- 뷰 로더는 웹팩의 로더 종류 중 하나이고, 뷰 CLI로 프로젝트를 생성하면 기본적으로 설정됨


---
- [배동훈 - vue.js입문 초보 실전 웹앱 개발-1부](https://www.inflearn.com/course/real-%EC%9B%B9%EC%95%B1-%EA%B0%9C%EB%B0%9C-vuejs-1%EB%B6%80)
- [캡틴판교 - Vue.js 입문서](https://joshua1988.github.io/web-development/vuejs/vuejs-tutorial-for-beginner/)
- [마기의 개발 블로그 - MVC,MVP,MVVM 비교](https://magi82.github.io/android-mvc-mvp-mvvm/)
- [cracking vue.js](https://joshua1988.github.io/vue-camp/vue/sfc.html#%EC%8B%B1%EA%B8%80-%ED%8C%8C%EC%9D%BC-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%9D%98-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC)