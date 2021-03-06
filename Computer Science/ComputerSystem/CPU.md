# 중앙처리장치 Central Processing Unit

- 컴퓨터에서 데이터 처리 동작을 수행하는 부분
- 레지스터 세트 + 산술논리장치(ALU) + 제어장치(Control Unit)으로 구성
    - Register set : 명령어를 실행하는데 필요한 데이터를 보관
    - Control : RS간 정보전송 감시, ALU에게 수행할 동작을 지시
    - ALU : 명령어를 실행하기 위한 마이크로 연산 수행

## 레지스터들의 명칭과 기능
|레지스터 | 역할 |
|---|:---|
| `프로그램 계수기(Program counter)` |다음에 수행될 명령어가 들어있는 주기억장치의 주소를 기억= IC(instruction counter) or LC(location counter)|
| `명령 레지스터(Instruction Register)` | 프로그램 계수기가 지정하는 주소에 기억되어 있는 명령어를 해독하기 위해 임시 기억|
| `작업 레지스터(working register)` |산술논리연산을 실행할 수 있도록 자료를 저장하고 그 결과를 저장 - GPR과의 차이점은 ALU에 연결되어 있나없나의 차이|
| `상태 레지스터(status register)` | CPU의 상태를 나타내는 특수목적의 레지스터 - 연산결과의 상태, Zero, S(부호), V(오버플로우), C(캐리), I(인터럽트)|

## [CPU 내부 구조](https://velog.io/@underlier12/%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-09-CPU-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0%EC%99%80-%EB%A0%88%EC%A7%80%EC%8A%A4%ED%84%B0)

## 명령어 구성과 실행
### 레지스터 전송 언어
- 마이크로연산 : 레지스터에 저장된 데이터의 조작을 위해 실행되는 동작, 하나의 클럭 펄스 내에서 실행되는 기본적인 동작(ex - shift, count, clear, road, ...)

### CPU 디자인
- CPU 내의 다양한 디바이스들간 상호연결
    - 직접연결 : 연결 복잡도가 장치수의 제곱에 비래
    - 버스연결 : 공용선에 의한 연결 -> 가장 가성비가 높다, 관리를 위한 다양한 방법이 제시된다(ex - 멀티플렉서, 3상태버스연결)
    
## 마이크로 명령과 ALU
- 마이크로 연산은 레지스터에 저장된 데이터에 대해 수행되는 기본적인 연산으로 디지털 컴퓨터에서 흔히 사용되는 마이크로 연산은 다음과 같이 네 가지로 분류된다
    - 레지스터 사이에서 이진 정보를 전송하는 레지스터 '전송' 마이크로 연산
    - 레지스터에 저장된 수치 데이터에 대해 산술 연산을 수행하는 '산술' 마이크로 연산
    - 레지스터에 저장된 비수치 데이터에 대해 비트 조작 연산을 수행하는 '논리' 마이크로 연산
    - 레지스터에 저장된 데이터에 대해 시프트 연산을 수행하는 '시프트' 마이크로 연산
- ALU : 산술연산(덧셈, 뺄셈, 곱셈, 나눗셈, 증가,감소,보수)과 논리연산(AND,OR,NOT,XOR,shift)

## 마이크로 명령어 집합과 구성
- 실행순서에 따른 명령어 분류
    - 순차적 실행 명령어
    - 분기 명령어
    - 부 함수 호출 명령어
    - 복귀 명령어

|설계관점|자연어에 가까운 명령 코드|기계 중싱의 명령코드|
|:---:|:---:|:---:|
|`프로그램관점`|프로그램이 용이, 전체 프로그램 길이 감소, 번역기 설계 용이|프로그래밍 규칙이 많아 짐, 프로그램길이 증가, 번역기의 설계가 복잡해짐|
|`CPU 구조 설계 측면`|사용언어에 따른 구조적 차이로 인한 오동작 및 처리 어려움, 명령어의 길이 증가, 제어장치의 제어가 매우 복잡|다양한 업체별 국가별 프로그래밍의 표준호나가 가능, 명령어의 종류 및 길이등 간편화될 수 있음, 제어장치 제어가 상대적으로 용이|

- 명령어 구문 형식
    1. 명령코드 : CPU가 실행할 수 있도록 디자인 된 연산
    2. 오퍼랜드 주소 : 연산에 사용되는 자료 값, 자료가 저장 된 주소에 관한 정보
    3. 주소지정모드 : 오퍼랜드가 저장된 위치를 인덱싱(지정)하는 방법   
    -> indirect 모드 : 소프트웨어와 하드웨어의 독립성 유지 
### 주소 지정 모드
- 명령어의 구조상 자료가 저장되어 있는 장소를 지정하는 방법이 필요함
- 최대한 하드웨어와 소프트웨어의 독립성을 유지해 프로그램의 유연성을 가능하게해 명령어의 수와 길이를 줄이기 위한 세계적 표준화 기법
- 묵시적 모드 : operand가 명령어에 포함되지 있지 않은 특수 모드
    - NOP : 오퍼랜드가 필요 없는 명령어
    - INP : 묵시적 오퍼랜드인 누산기의 연산 명령어
    - ADD : 스택 구조의 명령어(스택에 오퍼랜드가 저장)
- 메모리 간접 주소 모드 : 메모리를 이용하여 간접적으로 주소를 지정하는 모드

## 입출력
- 컴퓨터는 사용자와 통신을 하기 위해서 외부 장치, 즉 메모리로 데이터와 명령어를 읽어 들일 입력장치(input-device)와 계산결과를 사용자에게 표시해 줄 출력장치(output-device)를 갖추어야함
- input-output termianl -- Serial communication interface -- Computer registers and flip-flops

## 인터럽트
- 플래그를 사용한 통신 방법을 프로그램 제어 전송이라고 하는데 이것은 컴퓨터 실행 속도 대비 외부 입력 장치와의 입출력 속도차이 때문에 매우 비능률적
- IEN(interrupt enable flip-flop)
    - 프로그램 제어전송 대신에 외부장치가 전송 준비가 되었을 때 컴퓨터에 알리는 방법에 활용되는 플립플롭
    - 컴퓨터는 프로그램 실행 도중 플래그를 체크하지 않으며, 플래그가 세트되면 컴퓨터는 즉각 실행 중이던 프로그램을 중지하고 플래그의 세트정보를 받아들여 입출력을 실행/입출력 실행 후 즉시 원프로그램으로 복귀
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [컴퓨터구조 - 이승조]    
- [underlier12.log](https://velog.io/@underlier12/%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-09-CPU-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0%EC%99%80-%EB%A0%88%EC%A7%80%EC%8A%A4%ED%84%B0)