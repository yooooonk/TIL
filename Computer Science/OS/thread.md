# Thread 스레드

- Light Weight Process라고도 함
- 프로세스처럼 동작하지만 그것보다는 구조가 작다, 프로세스의 서브셋
- 하나의 프로세스에 여러개의 스레드 생성가능
- 스레드들은 동시에 실행 가능
- 프로세스 안에 있으므로, 프로세스의 데이터에 모두 접근 가능
- 스레드에는 각기 실행이 가능한 스택이 존재
    ![스레드](https://github.com/yooooonk/TIL/blob/master/img/thread.PNG)
- 멀티 테스킹과 멀티 프로세싱
    ![multiTasking&MultiProcessing](https://github.com/yooooonk/TIL/blob/master/img/multiTasking%26processing.PNG)

### 스레드의 장단점
- 장점
    - 사용자에 대한 응답성 향상
    - 프로세스 안에 있으므로 프로세스의 데이터에 모두 접근가능하기 때문에 스레드간 자원 공유를 위해 번거로운 작업이 필요없다
    - 작업이 분리되어 코드가 간결하다
- 단점
    - 스레드 중 한 스레드만 문제가 있어도 전체 프로세스가 영향을 받음
    - 스레드를 많이 생성하면 모든 스레드를 스케줄링해야 하므로 Context Switching이 많이 일어나, 성능 저하

## 스레드 동기화 
- 동기화 : 작업들 사이에 실행 시기를 맞추는 것
- 여러 스레드가 동일한 자원(데이터)에 접근할 때 각 스레드 결과에 영향을 줌
- 스레드가 실행되는 도중 context switching이 일어나 작업을 마치지 못한 상태에서 다른 스레드가 실행되기 때문
- Mutual exclusion(상호배제) : 어느 한 스레드가 공유 변수를 갱신하는 동안 다른 스레드가 동시 접근하지 못하도록 막는 것
``` python
import threading

g_count = 0

def thread_main() :
    num = 0
    global g_count
    look.acquire() # mutual exclusion - 파이썬에서 제공하는 함수
    for i in range(100000) : 
        g_count = g_count + 1
    lock.release()
lock = threaing.Lock()
threads = []        

for i in range(50):
    th = threading.Thread(target = thread_main)
    threads.append(th)

for th in threads :
    th.start()    

for th in theads : 
    th.join()    

print('g_count =',g_count)    
```

### Semaphore 세마포어
- Locking Machanism
    - Mutex(binary semaphore) : 임계구역에 하나의 스레드만 들어갈 수 있음
    - Semaphore : 임계 구역에 여러 스레드가 들어갈 수 있음
- 세마포어는 counter를 두어서 동시에 리소스에 접근할 수 있는 허용 가능한 스레드 수를 제어
    - S : 세마포어 값 - 초기 값만큼 여러 프로세스가 동시에 임계 영역 접근 가능
    - P : 검사(임계 영역에 들어갈 때) - S값이 1이상이면 임계 영역 진입 후 S값 1차감, S가 0이면 대기
    - V : 증가(임계 영역에서 나올 때) - S값을 1더하고, 임계 영역을 나옴

### 교착상태(Deadlock)과 기아상태(Starvatin)
- Deadlock
    - 무한대기상태
    - 두 개 이상의 작업이 서로 상대방의 작업이 끝나기 만을 기다리고 있기 때문에, 다음 단계로 진행하지 못하는 상태
    - 프로세스, 스레드 둘 다 이와 같은 상태가 나타날 수 있다
    - 여러 프로세스가 동일 자원 점유를 요청할 때 발생
- Starvation
    - 특정 프로세스의 우선순위가 낮아서 원하는 자원을 계속 할당 받지 못하는 상태
    - 여러 프로세스가 부족한 자원을 점유하기 위해 경쟁할 때, 특정 프로세스는 영원히 자원 할당이 안되는 경우를 주로 의미함
    

---
__reference__
- [패스트캠퍼스 컴퓨터공학 운영체제 - 이준희]