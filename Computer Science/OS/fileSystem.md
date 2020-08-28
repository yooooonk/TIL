# 파일 시스템 File System
- 운영체제가 저장매체에 파일을 쓰기 위한 자료구조 또는 알고리즘
- _동일한 시스템콜_ 을 사용해서 다양한 파일 시스템 지원을 가능하도록 구현 
    - read/write 시스템 콜 호출시, 각 기기 및 파일 시스템에 따라 실질적인 처리를 담당하는 함수를 구현
    - 파일이 실제 어떻게 저장할지는 운영체제마다 다를 수 있다

## inode 방식 파일 시스템
- 파일 시스템 기본 구조
    - 수퍼 블록 : 파일 시스템 정보 및 파티션 정보 포함
    - 아이노드 블록 : 파일 상세 정보
    - 데이터 블록 : 실제 데이터
- 파일은 inode 고유값과 자료구조에 의해 주요 정보 관리
    - '파일이름:inode'로 파일이름은 inode 번호와 매칭
    - 파일 시스템에는 inode를 기반으로 파일 엑세스
    - inode 기반 메타 데이터 저장
- inode구조
    ![inode구조](https://github.com/yooooonk/TIL/blob/master/img/innode%20structure.PNG)

    - inode 기반 메타 데이터 : 파일 권한, 소유자 정보, 파일 사이즈, 시간 관련 정보(생성시간 등), 데이터 저장 위치 등    
    - Direct blocks : 파일 내용, 12개정도의 주소 공간을 가짐, 실제 데이터 블럭의 주소를 가지고 있음
    - Indirect Block : 4KB에 direct block 주소를 가지고 있는 4byte 블럭의 주소를 1024개 저장 : 1024 * 4KB(direct block의 크기) = 4MB 저장
    - Double Indirect : 4KB에 single Indirect 주소를 1024개 저장 : 1024 * 1024 * 4kb = 4GB
    - Triple Indirect : 4KB에 double Inderet 주소를 1024개 저장 : 1024 * 1024 * 1024 * 4kb

## 가상 파일 시스템(Virtual File System)
![virtualFilesystem](https://github.com/yooooonk/TIL/blob/master/img/virtual%20file%20system.PNG)
- 파일 시스템 인터페이스를 통해 Network, IO device등 다양한 기기에서도 동일하게 관리 가능
- ex] read/writ 시스템콜 사용, 각 기기별 read_spec/write_sprc코드 구현(운영체제 내부)



---
__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]