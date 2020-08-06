# HTML
## Layout 태그
- header,nav,section,aside,body,footer 등이 있다
- 브라우저 호환성 문제때문에 div tag에 id를 줘서 사용하기도 함

## HTML 구조설계
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
  <header>
  <h1>Company Name</h1>
  <img src="..." alt="logo">
  </header>
  
  <div>  
    <nav><ul>
      <li>Home</li>
      <li>Home</li>
      <li>About</li>
      <li>Map</li>
      </ul></nav>
    
    <div>  
      <button></button>
      <div><img src="dd" alt=""></div>
      <div><img src="dd" alt=""></div>
      <div><img src="dd" alt=""></div>
      <button></button>
    </div>
    <div>
      <ul>
        <li>
          <h3>What we do</h3>
          <div>Lorem ipsum dolor sit amet, consectetur adipisicing</div>
        </li>
        <li>
          <h3>What we do</h3>
          <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Similique accusamus, corporis, dolorum fugiat tenetur porro. Aspernatur commodi, ea suscipit non? Molestiae nulla explicabo debitis provident nostrum dolorem minima reiciendis suscipit?</div>
        </li>
        <li>
          <h3>What we do</h3>
          <div>Lorem ipsum dolor sit amet, consectetur adipisicing</div>
        </li>
      </ul>
    </div>
  </div>
  <footer>
    <span>Copyright @codesquad</span>
  </footer>
</body>
</html>
```
## Class와 Id
- class는 하나의 HTML 안에 중복해서 여러 군데 사용가능, 보통 같은 스타일을 갖기위해
- id는 고유한 속성이므로 하나만 써야함

---
- [edwith 부스트코스 웹 프로그래밍](https://www.edwith.org/boostcourse-web/lecture/16668/)