# 운영체제
- 응용 프로그램이 요청하는 시스템 리소스를 효율적으로 분배하고 지원하는 소프트웨어
- 사용자가 사용하는 응용 프로그램이 효율적으로, 적절하게 동작하도록 지원한다
1. 시스템 자원관리
    - 각 프로그램이 CPU를 얼마나 사용하는지
    - 각 프로그램이 어느정도의 memory 공간을 확보해 어느 주소에 저장되어야 하는지
    - 어떤 저장매체에 어떻게 저장할지
    - 입력 받은 데이터를 어떤 프로그램에서 어떤식으로 보여줄지
2. 사용자와 컴퓨터 간의 커뮤니케이션
3. 컴퓨터 하드웨어와 응용 프로그램을 제어
    - ex] 응용 프로그램 실행, 권한관리, 사용자관리, ..    
![os](https://github.com/yooooonk/TIL/blob/master/img/os.PNG)
![os2](https://github.com/yooooonk/TIL/blob/master/img/osTotal.PNG)
## 발전과정
- 1950년대 
    - ENIAC : 최초의 컴퓨터, 운영체제 없이 응용프로그램이 직접 자원관리
- 1960년대
    - 프로그램 종류도 많아지고, 사용자도 많아지기 시작
    - __배치처리시스템__ : 여러 응용 프로그램을 등록시켜놓으면, 순차적으로 실행하는 시스템, 응답시간, 실행시간이 길다. 
    - __시분할 시스템__: 응용 프로그램이 CPU를 점유하는 시간을 잘게 쪼개어 실행할 수 있도록 하는 시스템, 응답시간이 짧다, 다중사용자 지원
    - __멀티테스킹__ : 단일 CPU에서 여러 응용 프로그램의 병렬 실행을 가능하게 하는 시스템. 시간을 아주 잘개 쪼개서 동시에 실행되는것처럼 보인다
    - _멀티프로그래밍_
- 1970년대
    - &#10024; __UNIX__ : 현대 운영체제의 기본 기술(멀티태스킹, 시분할, 멀티프로그래밍, ...)을 모두 포함한 최초의 운영체제
- 1980년대
    - PC의 등장 (이전에는 대형컴퓨터에 여러명이 접속해서 사용하는 형태)    
    - CLI -> GUI
- 1990년대
    - GUI 응용 프로그램이 많아짐
    - windows OS의 대중화
    - 네트워크의 발전
    - 오픈소스운동 전개 - Linux
- 2000년대
    - 오픈소스활성화 : Linux, Apache, mySQL, ...
    - 가상 머신, 대용량 병렬 처리등 활성화        
    
## 구조
![osstructure](https://github.com/yooooonk/TIL/blob/master/img/userinterface.PNG)

### 사용자 인터페이스
- shell : 사용자가 운영체제 기능과 서비스를 조작할 수 있도록 인터페이스를 제공하는 프로그램
- CLI, GUI
### 응용프로그램 인터페이스    
- 시스템콜 : 운영체제의 각 기능을 응용 프로그램이 사용할 수 있도록 제공하는 명령어
- API는 내부에서 시스템콜을 호출하는 형태로 만들어짐

## CPU Protection Rings
- CPU에는 권한 모드가 있음
- 응용프로그램이 전체 컴퓨터 시스템에 영향을 주지 못하도록 보호하기 위함
    - 사용자모드 : 응용프로그램이 사용
    - 커널 모드 : 특권 명령어 실행과 원하는 작업 수행을 위한 자원 접근을 가능하게 하는 모드, OS가 사용, 커널모드로 실행하려면 반드시 시스템콜을 사용해야 함
    ![protectionrings](https://github.com/yooooonk/TIL/blob/master/img/protectionring2.png)
``` C
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

int main(){
    int fd;
    fd = open("data.txt",O_RDONLY); // open() 시스템 콜 호출 -> 커널모드로 전환 
    //-> open() 함수를 처리하는 sys_open() 커널 함수 호출 -> 파일 열기의 law level 연산 수행 
    //-> 사용자모드로 전환 -> open() 함수 이후의 프로그램을 이어서 실행

    if(fd == -1){
        printf("Error : can not open file\n");
        return 1;
    }else{
        printf(*File opned and now close_\n*);
        close(fd);
        return();
    }
    
}

```    
---
__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]