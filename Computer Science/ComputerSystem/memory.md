# 메모리
- 메모리 장치란 data의 _저장_ 과 _접근_ 을 용이하게 하기위해 필요로 하는 장치

## 메모리 계층
- CPU에 의해 시행될 프로그램이 저장되는 곳
- 메모리 간의 속도 차이가 나기 때문에 전체 시스템을 효율적으로 사용하기 위해 메모리 계층을 나눔
- 종류
    - 주기억장치 : RAM, ROM 
    - 캐쉬 메모리(buffer) : 현재 진행되고 있는 프로그램의 일부 또는 사용빈도가 높은 임시데이터 저장
    - 보조기억장치 : 비교적 저속, 대용량의 자료보관이 가능, 보조기억장치 내에 자료는 필요한 경우 주 기억장치로 옮겨짐(Loading)

![페스트캠퍼트 컴퓨터 구조 memory system의 이해](https://github.com/yooooonk/TIL/blob/master/img/memory.PNG)
![ljh0326s](https://github.com/yooooonk/TIL/blob/master/img/memory%20layer.PNG)

## 주기억장치
- RAM의 동작원리  
![패스트캠퍼스 컴퓨터구조 memery system의 이해](https://github.com/yooooonk/TIL/blob/master/img/ram.PNG)

## Associative 메모리
- 내용에 의해 접근하는 메모리 장치 = CAM
- 데이터의 내용으로 __병렬 탐색__ 을 하기에 적합하도록 구성되어 있음
- 탐색은 전체 워드 또는 한 워드 내의 일부를 가지고 실행할 수 있음
- 각 셀이 저장능력 뿐 아니라 외부의 인자와 내용을 비교하기 위한 _논리회로_ 를 갖고 있기 때문에 RAM보다 값이 비쌈
- 따라서 탐색시간이 반드시 짧아야하고 중요한 이슈일경우 활용

## Cache 메모리
![cache](https://github.com/yooooonk/TIL/blob/master/img/cache.PNG)
- CPU의 처리속도와 주기억장치의 접근 속도 차이를 줄이기 위해 사용하는 고속 Buffer Memory
- 메인메모리와 cpu의 중간에 위치
-참조의 국한성 : 프로그램이 수행되는 동안 메모리 참조는 국한된 영역에서만 이루어지는 경향이 있음 = 자주 사용하는 프로그램과 데이터를 기억함 
- 주기억장치에 접근하는 횟수가 줄어들어 컴퓨터의 처리속도가 향상됨
- 기본동작
    - hit : 워드가 cache에서 발견되면 읽어들임
    - miss : 없으면 주기억장치에 접근
- 성능을 높이려면 hit ratio를 높이고, 캐쉬를 재구성(삭제)을 효율적으로 해야함

### Cache Mapping
- 효율적인 메모리 관리를 위해 cache를 구성하는 방법
- __Direct mapping__ 
    - 주기억장치의 블록들이 지정된 한 개의 캐시 라인으로만, 간단하고 구현비용이 적게들지만 히트율이 낮아질 수 있음
- __Associative Mapping__ 
    - _주소_ 와 같은 12bit의 데이터를 읽어서 cpu로 보냄
    - miss인 경우 cpu는 주기억장치에서 해당 자료를 찾아 cache로 옮김
    - cache가 꽉 차있을 경우 기존 cache의 주소와 데이터쌍 중 주어진 알고리즘에 의해 해당 주소 데이터쌍이 새로운 쌍으로 대체 됨
    - 모든 태그들을 병렬로 검사하기 때문에 복잡하고 비용이 높음
    - Set-Associative Mapping : 직접매핑과 연관 매핑의 장점만
    

## 효율적인 메모리 관리 정책

---
__reference__
 - fastcampus 컴퓨터 공학 전공 필수 [컴퓨터구조 - 이승조]    
 -[ljs0326블로그 - 기억장치](http://blog.naver.com/PostView.nhn?blogId=ljh0326s&logNo=220851633811)
 - [코딩팩토리 - 캐시메모리란 무엇인가?](https://coding-factory.tistory.com/357?category=828008)