# 가상 메모리 Virtual Memory
- 폰노이만 구조는 메모리에 코드가 반드시 올라가있어야하는데, 실제 각 프로세스마다 충분한 메모리를 할당하기에는 메모리 크리에 한계가 있음
- 가상메모리는 메모리가 실제 메모리보다 많아 보이게 하는 기술
- 프로세스간 공간 분리로, 프로세스 이슈가 전체 시스텀에 영향을 주지 않을 수 있음
- 프로세스는 가상 주소를 사용하고, 실제 해당 주소에서 데이터를 읽고 쓸때만 물리 주소로 바꿔주면 된다
    - 가상주소(virtual address) : 프로세스가 참조하는 주소
    - 물리주소(physical address) : 실제 메모리 주소
- MMU : CPU에 코드 실행시, 가상 주소 메모리 접근이 필요할 때, 해당 주소를 물리 주소값으로 변환해주는 하드웨어 장치
    ![mmu](https://github.com/yooooonk/TIL/blob/master/img/mmu.PNG)

## 페이징 시스템 Paging System
![페이징시스템](https://github.com/yooooonk/TIL/blob/master/img/paging%20system.PNG)
- 크기가 동일한 페이지로 가상 주소 공간과 이에 매칭하는 물리 주소 공간을 관리
- 하드웨어 지원이 필요하다
- 페이지 번호를 기반으로 가상 주소/물리주소 매핑 정보를 기록
- 프로세스의 PCB에 Page Table 구조체를 가리키는 주소가 들어 있음
- Page Table
    - 가상 주소와 물리 주소간 매핑 정보가 있음
    - 가상주소 v = (p,d)라면 p는 페이지 번호, d는 페이지 처음부터 얼마나 떨어져있는지
- 동작
    - 해당 프로세스의 page table에 해당 가상 주소가 포함된 page 번호가 있는지 확인
    - page 번호가 있으면 이 page가 매핑된 첫 물리 주소를 알아내고(p')
    - p'+d가 실제 물리 주소가 됨
- 페이징 시스템과 MMU
    - CPU는 가상 주소 접근시 MMU 하드웨어 장치를 통해 물리 메모리 접근
    - 프로세스 생성시, 페이지 테이블 정보 생성
        - PCB등에서 해당 페이지 테이블 접근 가능하고, 관련 정보는 물리 메모리에 적재
        - 프로세스 구동시, 해당 페이지 테이블 base 주소가 별도 레지스터에 저장(CR3)    
        - CPU가 가장 주소 접근시, MMU가 페이지 테이블 base 주소를 접근해서 물리주소를 가져옴
- 선행 페이징 : 미리 프로세스 관련 모든 데이터를 메모리에 올려놓고 실행
- 요구 페이징
    - 프로세스의 모든 페이지를 메모리에 올리지 않고, 실행 중 필요한 시점에서만 메모리도 적재함
    - 더 이상 필요하지 않은 페이지 프레임은 다시 저장매체에 저장(페이지 교체 알고리즘 필요)

### 다중 단계 페이징 시스템
- 페이징 정보를 단계를 나누어 생성 - 필요없는 페이지는 생성하지 않으면, 공간 절약 간으

### 페이지 폴트 Page fault
- 페이지 폴트는 어떤 페이지가 실제 물리 메모리에 없을 때 일어나는 인터럽트
- page fault가 일어나면 운영체제가 해당 페이지를 물리 메모리에 올림
- 페이지 폴트가 자주 일어나면 실행되기 전에 해당 페이지를 물리 메모리에 올려야 한다. 시간이 오래 걸림
- __스레싱 Thrashing__
    - 반복적으로 페이지 폴트가 발생해서, 과도하게 페이지 교체 작업이 일어나, 실제로는 아무일도 하지 못하는 상황

### 페이지 교체 알고리즘
- FIFO : 가장 먼저 들어온 페이지를 교체
- OPT : 앞으로 가장 오랫동안 사용하지 않을 페이지를 교체, 일반 OS에서는 구현불가
- LRU : 가장 오래전에 사용한 페이지를 교체
- LFU : 가장 적게 사용한 페이지를 교체
- NUR : LRU와 마찬가지로 최근에 하용하지 않은 페이지를 교체, 각 페이지마다 참조비트(R), 수정비트(M)를 둠

## Segmentation 기법
- 가상 메모리를 서로 크기가 다른 논리적 단위인 세그먼트로 분할
- 페이징 기법에서는 가상 메모리를 같은 크기의 블록으로 분할



---
__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]