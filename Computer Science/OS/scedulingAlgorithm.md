# 프로세스 스케줄링 알고리즘

- 프로세스 : 메모리에 올려져서 실행 중인 프로그램. 응용 프로그램 != 프로세스
- 코드이미지(바이너리) : 실행파일  ex] elf format

## 스케줄링 알고리즘?
- 어느 순서대로 프로세스를 실행시킬 것인가
- 목적 : 짧은 응답시간,  CPU 활용도 높임, 빠른 프로세스 실행 등

### FIFO 스케줄러
- 가장 간단한 스케줄러(배치처리시스템)
- First Come First Served

### SJF 스케줄러
- Shortest Job First
- 프로세스 실행시간이 가장 짧은 것부터 실행

### 우선순위 기반 스케줄러
- 정적 우선순위 : 프로세스마다 우선순위를 미리 지정
- 동적 우선순위 : 스케줄러가 상황에 따라 우선순위를 동적으로 배정

### Round Robin 스케줄러
- FIFO로 실행된 후 일정 시간이 지나면 다시 queue로 돌아감
- 시분할 시스템 기반

## 프로세스 상태와 스케줄링
- 프로세스 상태정보
    - 프로세스 생성
    - 실행가능(ready) : CPU에서 실행 가능한 상태
    - 실행중(running) : 현재 CPU 실행상태
    - 대기(blocked) : 특정 이벤트 발생 대기 상태 ex] 프린팅 완료, 파일 읽기 완료
    - 종료

### 프로세스 상태기반 스케줄링 알고리즘
- StateQueue
    - Ready State Queue
    - Running State Queue
    - Block State Queue

## 선점형과 비선점형 스케줄러
- 선점형(Preemptve Scheduling) : 하나의 프로세스가 다른 프로세스 대신에 프로세서를 차지할 수 있음 ex] Round Robin
- 비선점형(Non-preemptive Sheduling) : 하나의 프로세스가 끝나지 않으면 다른 프로세스는 CPU를 사용하지 않는다. 프로세스가 자발적으로 blocking 상태로 들어가거나 실행이 끝났을 때만 다른 프로세스로 교체가능. ex] FIFO, SJF, Priority-based.


---
__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]