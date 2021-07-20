# 실행 컨텍스트

실행 컨텍스트란 __실행할 코드에 제공할 환경 정보들은 모아놓은 객체__ 로, 자바스크립트 엔진이 사용할 목적으로 생성한다. 자바스크립트는 어떤 실행 컨텍스트가 활성화되는 시점에 선언된 변수를 호이스팅하고, 외부 환경 정보를 구성하고, this 값을 설정한다. 

- 하나의 실행 컨텍스트를 구성할 수 있는 방법 : 전역공간, eval() 함수, 함수 등
- 자바스크립트 코드를 실애하는 순간 전역 컨텍스트가 콜 스택에 담긴다.
- 전역 컨텍스트는 코드 내부에서 별도의 실행 명령이 없어도 브라우저에서 자동으로 실행되기 때문에 자바스킙트 파일이 열리는 순간 전역 컨텍스트가 활성화된다고. 

## 실행 컨텍스트에 저장되는 정보들
## Variable Environment
담기는 내용은 LexicalEnvironment와 같다. 그러나 최초 실행 시의 스냅샷을 유지한다는 점이 lexical Environment와 같다.

## LexicalEnvironment
### EnvironmentRecord
현재 컨텍스트와 관련된 코드의 식별자 정보들(매개 변수 식별자, 함수 자체, 변수 식별자)가 저장된다.
컨텍스트 내부 전체를 전체부터 끝까지 순서대로 훑어나가며 수집(호이스팅)한다. 식별자 정보 수집은 실행 컨텍스트가 관여할 코드를 실행하기 전에 모두 마친다.

호이스팅 : 변수 정보 수집 과정을 이해하기 쉬운 방법으로 대체한 가상 개념. 자바스크립트 엔진이 실제로 식별자들을 최상단으로 끌어올리지는 않지만 편의상 끌어올린 것으로 간주하기 위함으로 만들어진 개념이다.

### Outer Environment Lexical
스코프란 식별자에 대한 유효범위

스코프 체인이랑 식별자의 유효범위를 안에서부터 바깥으로 차례로 검색해나가는 것

전역 컨텍스트의 LexicalEnvironment에 대한 담긴 변수를 

### This Binding

---
__📑 referece__