# 비동기처리

## 비동기?
- 특정 코드의 연산이 끝날 떄까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성
- 서버로 요청을 보내고 응답이 오면 다음 코드를 실행하는 동기처리로 하면 웹 어플리케이션을 실행하는데 시간이 오래걸릴 수 있음
- 비동기의 예 : ajax, setTimeout()
``` java script
// ajax
function getData(){
    var tableData;
    $.get('url',function(res){
        tableData = res;
    });

    return tableData;
}

console.log(getData()) // undefined

// setTimeout()
console.log('1. hello');

settimeout(function(){
    console.log('2.bye')
},3000);

console.log('3.hello again')

// 1. hello
// 3. hello again
// 2. bye
```

## 콜백함수
- 서버에서 받은 데이터를 callback 함수로 넘겨주는 방식
- 비동기 처리를 위해 콜백함수를 연속해서 사용해야할 경우 콜백 안에 콜백을 계속 무는 형식이 되어 가독성이 떨어지고 로직을 변경하기도 어렵다 -> 콜백지옥
```
function getData(callbackFunc){
    var tableData;
    $.get('url',function(res){
        callbackFunc(res)
    });

    return tableData;    
}

getData(function(tableData){
    console.log(tableData); //$.get()의 res 값이 tableData에 전달됨
})
```
ex] 콜백지옥
``` javascript
$.get('url',function(res){
    parseValue(res,function(id){
        auth(id,function(result){
            display(result,function(text){
                console.log(text);
            })
        })
    })
})
// 해결
function parseValueDone(id){
    auth(id,authDone);
}
function authDone(result){
    dispaly(result,displayDone);
}
function displayDone(test){
    console.log(text);
}

$.get('url',function(res){
    parseValue(res,parseValueDone);
})
```

## Promise
- 자바스크립트 비동기 처리에 사용되는 객체
- 프로미스는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용
- new Promise()로 객체를 생성하면 콜백 함수 인자로 resolve와 reject를 사용할 수 있다
- 프로미스 상태
    - 대기(pending)
    - 이행(fulfilles) : resolve를 하면 이행상태가 됨 -> .then()을 이용해 처리결과 값을 받을 수 있다
    - 실패(rejected) : reject를 호출하면 실패상태-> .catch()로 받을 수 있다    
- _promise chaining_ : 여러 개의 프로미스를 연결하여 사용할 수 있음. _then()_ 을 호출하고 나면 새로운 프로미스 객체가 반환되기때문
``` javascript
// 콜백
function getData(callbackFunc){
    $.get('url주소',function(res){
        callbackFunc(res);
    });        
}
getData(function(tableData{
        console.log(tableData);
    }))

// 프로미스
function getData(callback)    {
    // new promise 추가
    return new Promise(function(resolve,reject){ // 대기상태
        $.get(url,function(res){
            if(response){ // 데이터를 받으면 resolve()호출
                resolve(res); // 이행
            }
            reject(new Error("에러메세지"));
        })        
    });
}

getData2.then(function(tableData){// resolve의 결과값이 여기로 전달됨    
    console.log(tableData)
}).catch(function(err){
    console.error(err) // 에러메세지 출력
})
```    
``` javascript
// 프로미스 체이닝
new Promise(function(resolve, reject){
  setTimeout(function() {
    resolve(1);
  }, 2000);
})
.then(function(result) {
  console.log(result); // 1
  return result + 10;
})
.then(function(result) {
  console.log(result); // 11
  return result + 20;
})
.then(function(result) {
  console.log(result); // 31
});
```