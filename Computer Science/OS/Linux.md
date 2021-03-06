
# Linux
- 리누스 토발즈가 커뮤니티 주체로 개발한 UNIX 계열의 컴퓨터 운영체제
- 다중 사용자, 멀티태스킹, 다중 스레드를 지원하는 네트워크 운영체제다
- 오픈소스이기 때문에 다양한 리눅스 기반의 운영 체제가 있다.   
    ex] 페도라, 우분투, 안드로이드 
- pc에서 linux의 점유율은 낮지만 슈퍼컴퓨터, 모바일, 임베디드 등의 영역에서는 linux의 점유율이 매우 높다
- GNU : Gnu is Not Unix
    - 리차트 스톨만이 초기 컴퓨터 개발 공동체의 상호협력적인 문화로 돌아갈 것을 주장하며, 1985년도에 GNU 선언문을 발표
    - GNU 프로젝트를 지원하기 위해 자유 소프트웨어 재단 설립과 GNU 공개 라이선스(GPL)라는 규약을 제공
    - 운영체제에 필요한 라이브러리, 컴파일러, 에디터, 쉘 개발

### 파일
- 모든 것은 파일이라는 철학을 따름
    - 모든 인터렉션은 파일을 읽고, 쓰는 것처럼 이루어져 있음
    - 마우스, 키보드와 같은 모든 디바이스 관련된 기술도 파일과 같이 다루어짐
- 파일 네임스페이스
    - 전역 네임 스페이스를 제공
- 파일은 inode 고유값과 자료구조에 의해 주요 정보 관리

### 프로세스
- ELF : 리눅스 실행 파일 포멧
    - 콜스택, 코드, 데이터 및 BSS 섹션 등
- 시스템콜 호출을 통해 리소스 처리가 가능하다
    - 타이머, 시그널, 파일, 네트워크, 디바이스, IPC 기법
- 가상 메모리 지원
- 각 프로세스는 pid(프로세스id) 고유값으로 구분

### 권한
- 리눅스는 사용자/그룹
- root는 슈퍼관리자
- 파일마다 소유자, 소유자 그룹, 모든 사용자에 대해 읽고, 쓰고, 실행하는 권한을 관리
- 접근 권한 정보는 inode의 자료구조에 저장

### 쉘 Shell
- 사용자와 운영체제간 인터페이스
- 사용자의 명령을 해석해서, 커널에 요청해주는 역할
- 간련된 시스템콜을 사용해서 프로그래밍이 작성되어 있음
- GUI와 CLI 환경이 있음
- 종류
    - bash(Bourne-Again Shell) : GNU 프로젝트의 일환으로 개발됨, 리눅스에서 거의 기본적으로 쓰임
    - sh(bourne Shell) 
    - C shell
    - Korn shell : 유닉스에서 가장 많이 사용됨

---
__reference__
- [wikipedia - Linux](https://ko.wikipedia.org/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4)
- [왜 우리는 리눅스를 배워야 하는가](https://www.youtube.com/watch?v=TZjB94sA3IU)
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]