# 프로세스 스케줄링

## 배치 처리 시스템
- 자동으로 다음 응용 프로그램이 실행될 수 있도록
- 순차실행 -> 실행 시간이 긴 프로그램이 앞에 있으면 다른 프로그램 응답시간이 길어진다

## 시분할
- 응용 프로그램이 CPU를 점유하는 시간을 잘게 쪼개어 실행될 수 있도록 하는 시스템
- 응답시간이 짧아진다

## 멀티 태스킹
- _단일 CPU_ 에서 여러 응용 프로그램이 동시에 실행되는 것처럼 보이도록 하는 시스템
ex] 음악들으면서 문서작성 : 음악 - 문서 - 음악 - 문서 - ...
- 10~20ms 단위로도 실행 응용 프로그램이 바뀌므로 사용자에게는 동시에 실행되는 것처럼 느껴짐
- 시분할 시스템의 기본 기술과 같다

## 멀티 프로세싱
- _여러 CPU_ 에 하나의 프로그램을 병렬로 실행해서 실행속도를 극대화함

## 멀티 프로그래밍
- 단위 시간당 CPU를 활용도를 높이는 기술
- 응용 프로그램은 실행되는 동안 온전히 CPU를 쓰지않고 중간에 다른 작업을 하는 경우가 있다. 
ex] 프로그램 실행중에 파일을 읽거나 프린트하는 경우
- 다른 작업을 하는 동안 다른 프로그램을 cpu에서 실행

---
__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]