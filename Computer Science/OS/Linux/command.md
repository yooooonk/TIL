# 리눅스 명령어

- __sudo__ : (super user) 현재 계정에서 root 권한을 이용해 명령어를 실행할 때 사용

- __yum__ : (Yellowdog Updater Modified) RPM 기반의 시스템을 위한 자동 업데이터이자 소프트웨어와 같은 패키치 설치/삭제 도구, RPM과 달리 자동적으로 의존성을 처리해주며 rpm 패키지들을 안전하게 설치, 삭제 및 업데이트하기 위해 반드시 해야 할 일을 스스로 해결.
    |명령어/옵션|의미|예시|
    |--|--|--|
    |install|시스템으로 패키지의 install을 실시|yum install java-1.8.0-openjdk-devel.x86_64|
    |list|서버에 있는 그룹 및 패키지의 리스트를 보여줌|yum list java*jdk-devel|

- __rm__ : (remove)

- __ln__ : (link) 파일시스템에서 링크파일을 만드는 명령어
    |명령어/옵션|의미|예시|
    |--|--|--|
    |-s|심볼릭 링크파일 생성|ln -s /usr/share/zoneinfo/Asis/Seoul /etc/localtime|