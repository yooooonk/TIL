

# Hook
> Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동“할 수 있게 해주는 함수입니다. 

## 목적
- 전형적인 React는 컴포넌트 사이에서 상태와 관련된 로직을 재사용하기 어렵다. 이를 해결하기 위해 render props나 고차 컴포넌트와 같은 패턴을 사용해야한다면, 컴포넌트를 재구성해야하고 코드를 추적하기 어렵다.  Hook을 사용하면 컴포넌트로부터 상태 관련 로직을 추상화할 수 있고, 독립적인 테스트와 재사용이 가능하다. __Hook은 계층 변화 없이 상태 관련 로직을 재사용할 수 있도록 도와준다.__

- class형 컴포넌트에서는 상태 관련 로직과 사이드 이펙트가 분리되지않아 life cycle method(compoonentDidMount,componentDidUpdate,componentWillUnmount)에 관련 없는 로직이 섞여 있다. 함께 변경되는 상호 관련 코드는 분리되지만, 이와 연관 없는 코드들은 단일 메서드로 결합해 버그가 쉽게 발생하고 무결성을 해친다. 상태 관련 로직이 모든 공간에 있기 때문에 컴포넌트들을 작게 만드는 것이 불가능하고 테스트하기도 어렵다. 이를 해결하기 위해 생명주기 메서드를 기반으로 쪼개기 보다는 __Hook을 통해 로직에 기반을 둔 작은 함수로 컴포넌트를 나눌 수 있다__

## 규칙
- 최상위에서만 Hook을 호출해야 한다
- React 함수 내에서만 Hook을 호출해야 한다.
- 사용자정의 Hook 이름은 use로 시작되어야 한다

## useState
``` javascript
const [value, setValue] = useState(null)
```
- 함수 컴포넌트 안에서 state를 사용할 수 있다.

- useState의 인자로 state의 초기 값을 넘겨준다. 클래스와 달리 객체일 필요는 없고, 숫자 타입과 문자 타입을 가질 수 있다. 
- state변수, 해당 변수를 갱신할 수 있는 함수 이 두 가지 쌍을 반환한다. 
- 컴포넌트가 렌더링할 때 오직 한 번만 생성된다

## useEffect
``` javascript
useEffect(()=>{
   // 리액트가 DOM을 업데이트한 뒤 추가로 실행하는 코드   
	return ()=>{
    	// clean up
    }
})
```

- 함수 컴포넌트 안에서 컴포넌트가 렌더링 된 이후에 side effect를 수행할 수 있다
- `side effect` : 데이터 가져오기, 구독설정하기, 수동으로 리액트 컴포넌트의 DOM을 수정하는 것등
- useEffect를 컴포넌트 내부에 둠으로써 effect를 통해 state와 props에도 접근할 수 있다
- 기본적으로 첫번째 렌더링과 이후의 모든 업데이트에서 수행된다.

- 외부 데이터에 구독을 설정하는 경우 메모리 누수가 발생하지 않도록 clean-up해야 한다. useEffect에서는 함수를 반환하는 메커니즘으로 clean up을 구현해 구독의 추가 제거 로직을 가까이 묶어둘 수 있게 했다. 컴포넌트가 마운트 해제되는 때에 clean-up을 실행한다.
- useEffect는 렌더링이 실행될 때마다 실행된다. 
- multiple effect로 관심사를 구분할 수 있다.
- useEffect의 선택적 인수인 두 번째 인수로 배열을 넘기면, 그 인수가 리렌더링 시에 변경되지 않으면 effect를 건너뛰어 성능 최적화가 가능하다.


### 사용자 정의 Hook
- 사용자 정의 Hook은 이름이 use로 시작하는 자바스크립트 함수.
- 사용자 Hook은 다른 hook을 호출할 수 있다
- 무엇을 인수로 받아야 하며 필요하다면 무엇을 반환해야 하는지를 사용자가 결정할 수 있다.
``` javascript
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```


---
__reference__
- https://ko.reactjs.org/docs/hooks-intro.html
- https://ko.reactjs.org/docs/hooks-state.html