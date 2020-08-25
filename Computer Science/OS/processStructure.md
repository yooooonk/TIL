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


---
__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]