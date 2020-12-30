# Jest
- FaceBook이 만든 테스팅 프레임 워크
- 최소한의 설정으로 동작하며 Test Case를 만들어서 어플리케이션 코드가 잘 돌아가는지 확인
- 단위테스트를 위해서 이용함

## 사용법
1. Jest 라이브러리 설치
``` 
npm install jest --save-dev
```
2. Test 스크립트 변경
3. 테스트 작성할 폴더 및 파일 기본 구조 생성
```
└ test
    └ unit
        └ xx.test.js
    └ intergration
```

### Jest가 Test 파일을 찾는 방법
- {filename}.test.js
- {filename}.spec.js
- test 폴더 내부

## Jest 파일
- dexscribe : 여러 관련 테스트를 그룹화하는 블록을 만듦
- it : 개별 테스트를 수행하는 곳, 각 테스트를 작은 문장처럼 설명
- expect : 값을 테스트할 때마다 사용됨, matcher와 함께 사용
- matchar : 다른 방법으로 값을 테스트하도록 
- beforeEach : 

- method
    - expect.toBe()
    - expect.toBeCalledWith(xx)
    - expect
    - res._isEndCalled()
    - mockReturnValue : 가짜 함수가 어떠한 결과값을 반환 할지 직접 알려줄 때 사용하는...