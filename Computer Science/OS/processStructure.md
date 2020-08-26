# 프로세스 구조
![프로세스 구조](https://github.com/yooooonk/TIL/blob/master/img/processStructure.PNG)

- STACK : 임시데이터(함수 호출, 로컬변수)
- HEAP : 코드에서 동적으로 만들어지는 데이터 ex]malloc()
- DATA : 변수/초기화된 데이터
    - BSS : 초기화되지 않은 변수
    - DATA : 초기값이 있는 전역 변수
- CODE(text) : 코드

ex]
``` c
// CODE
int global_data1; // DATA - BBS
int global_data2 = 1; // DATA - DATA
int main(){ //STACK
    int *data; // STACK
    data = (int*)malloc(sizeof(int)); // HEAP
    *data = 1;
    printf("%d\n",*data);
    return 0;  
}
```

## 프로세스와 컨텍스트 스위칭
- Context Swtiching : CPU에 실행할 프로세스를 교체하는 기술
- PCB : 프로세스 상태정보 - PC, SP, 메모리, 스케줄링 정보 등
- 실행 중지할 프로세스 정보를 해당 프로세스의  PCB에 업데이트에서 메인메모리에 저장
- 다음 실행할 프로세스 정보를 메인 메모리에 있는 해당 PCB 정보(PC,SP)를 CPU에 넣고 실행
![context switching](https://github.com/yooooonk/TIL/blob/master/img/contextSwitching.PNG)

## 프로세스간 커뮤니케이션(Inter Process Communication)
- 프로세스는 다른 프로세스의 공간에 접근할 수 없다 -- 프로세스 데이터/코드가 바뀌면 위험
- 프로세스간 통신이 필요한 이유?
    - 성능을 높이기 위해 여러 프로세스를 만들어서 동시에 실행
    - 프로세스간 상태 확인 및 데이터 송수신이 필요
- 프로세스간 공간은 완전 분리되어 있기 때문에 프로세스간 통신을 위해 특별한 기법이 필요함 --- IPC
- IPC는 커널 공간을 활용한 방법 - 커널 공간은 공유하기 때문

### 다양한 IPC기법
- PIPE
    ![pipe](https://github.com/yooooonk/TIL/blob/master/img/ipc_pipe.PNG)
    - 기본 파이프는 단방향 통신
    - fork()로 자식 프로세스 만들었을 때, 부모와 자식간의 통신
    - 커널 공간의 메모리를 사용
- Message Queue
    ![mesageQ](https://github.com/yooooonk/TIL/blob/master/img/ipc_messageQ.PNG)
    - Queue이므로 FIFO 정책으로 데이터 전송  
    - key 값을 알면 다른 프로세스의 데이터를 읽을 수 있다
    - 파이프와 달리 부모/자식이 아니라 어느 프로세스간에라도 데이터 송수신이 가능
    - 단방향, 양방향 모두 가능
    - 커널 공간의 메모리를 사용
- 공유 메모리
    - kernel space에 메모리 공간을 만들고, 해당 공간을 변수처럼 쓰는 방식
    - 공유메모리 key를 가지고 여러 프로세스가 접근 가능
    - message Queue처럼 FIFO 방식이 아니라, 해당 메모리 주소를 마치 변수처럼 사용
![커널공유](https://github.com/yooooonk/TIL/blob/master/img/ipc_%EC%BB%A4%EB%84%90%EA%B3%B5%EC%9C%A0.PNG)

- Signal
    - UNIX에서 30년 이상 사용된 전통적인 기법
    - 커널 또는 프로세스에서 다른 프로세스에 어떤 이벤트가 발생되었는지를 알려주는 기법
    - 프로세스 관련 코드에 관련 시그널 핸들러를 등록해서, 해당 시그널 처리 실행
        - 시그널 무시
        - 시그널 블록(블록을 푸는 순간, 프로세스에 해당 시그널 전달)
        - 등록된 시그널 핸들러로 특정 동작 수행
        - 등록된 시그널 핸들러가 없다면, 커널에서 기본 동작 수행
- Socket
    - 소켓은 네트워크 통신을 위한 기술
    - 기본적으로는 클라이언트와 서버등 두 개의 다른 컴퓨터 간의 네트워크 기반 통신 기술
    - 하나의 컴퓨터 안에서, 두 개의 프로세스 간에 통신 기법으로 사용 가능

---

__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]