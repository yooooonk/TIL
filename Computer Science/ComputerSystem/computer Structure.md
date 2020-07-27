# 컴퓨터의 구조
- 소프트웨어
    - 시스템 소프트웨어 -- 운영체제 : 응용 소프트웨어와 하드웨어 간의 호환성 문제 해결
    - 응용 소프트웨어
- 하드웨어
    - 입력장치
    - 처리장치
        - 주기억장치        
        - 중앙처리장치 : 제어장치, 연산장치    
    - 보조기억장치
    - 출력장치    

## 중앙처리장치 (Central Processing Unit)
- Mother Board : 데이터의 전달 통로가 디자인 되어있는 메인 보드
- 실행 프로그램의 명령 해석, 실행, 장치 제어, 기억 역할을 함
- 산술논리 연산 장치(ALU) + 제어장치(CU) + 각종 레지스터로 구성
- MPU(Micro Orocessor Unit)
    - CPU를 LSI(고밀도 집적회로)화 한 일종의 통합 장치
    - MPU의 등장으로 병렬처리, 멀티쓰레딩 등이 가능해짐
    - CISC(Complex Instruction set Computer) : 반복적인 처리를 하드웨어로 하겠다
    - RISC(Reduced Instruction Set Computer)

## 주변장치(Peripheral Device)
### 기억장치
- 주기억장치
    - RAM(Random Access Memory)
    - ROM(Read Only memory) :반적으로 한번 기록한 정보가 전원 유지와 상관없이 (반)영구적으로 기억되며, 삭제나 수정이 불가능한 기억 장치, 컴퓨터를 구동하기 위한 기본적인 정보가 담겨있다, 전력 공급과 무관하게 데이터가 유지되는 비휘발성이라는 강력한 특징이 있어서, 모든 종류의 기계에 쓰인다.
- 보조기억장치
    - HDD, SSD, USB, ...
- 주기억장치와 보조기억장치의 관계
    1. 전원 부팅시 CPU는 자동으로 ROM에 있는 프로그램 실행
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [컴퓨터구조 - 이승조]    
- [나무위키](https://namu.wiki/w/ROM)