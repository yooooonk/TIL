![](https://images.velog.io/images/ouo_yoonk/post/3bb65864-3123-4fab-9112-37de655bf458/styled-component%F0%9F%8E%A8.png)

# styled-component + typescript + nextjs

## Theme 파일 적용하기

```javascript
// theme.ts
import { DefaultTheme } from 'styled-components';

const theme: DefaultTheme = {
  color: {
    main: '#5D6E91',
    yellow: '#F9964f',
    gray: '#EEEDED',
    mainBlur: '#E7F0F9',
    mainThick: '#121B46'
  },
  view: {
    mobile: `(max-width: 767px)`,
    tablet: `(max-width: 1024px)`,
    desktop: `(min-width: 1025px)`
  },
  flex: {
    column:
      'display: flex; flex-direction:column; align-items: center; justify-content: space-between; ',
    row: 'display: flex; align-items: center; justify-content: space-between;'
  },
  border_box: `box-sizing:border-box;`
};

export default theme;
```

```javascript
//_app.tsx
import React from 'react';
import { AppProps } from 'next/app';
import { ThemeProvider } from 'styled-components';
import '../styles/reset.css';
import styled from 'styled-components';

// store
import wrapper from '../redux/configureStore';
import theme from 'styles/theme';

function App({ Component, pageProps }: AppProps) {
  return (
    <ThemeProvider theme={theme}>
      <React.Fragment>
        <Title>리액트</Title>
        <Component {...pageProps} />
      </React.Fragment>
    </ThemeProvider>
  );
}

const Title = styled.div`
  color: ${(props) => props.theme.color.main};
  font-size: 5rem;
`;

export default wrapper.withRedux(App);
```

## 컴포넌트 작성

```javascript
import React from 'react';
import styled from 'styled-components';

// 타입선언
type ButtonType = {
  disabled?: boolean,
  children: any,
  margin: boolean,
  width: string,
  padding: string,
  _onClick: () => void,
  color?: string
};

// 컴포넌트
const Button = (props: ButtonType) => {
  const { disabled, children, margin, width, padding, color, _onClick } = props;

  return (
    <ElButton {...props} onClick={_onClick}>
      {children}
    </ElButton>
  );
};
// default props
Button.defaultProps = {
  children: null,
  _onClick: () => {},
  is_float: false,
  margin: '0',
  width: '100%',
  padding: '12px 0px'
};

// styled-component
const ElButton =
  styled.button <
  ButtonType >
  `
  width: ${(props) => props.width};
  background-color: ${(props) => props.theme.main_color};
  color: #ffffff;
  padding: ${(props) => props.padding};
  box-sizing: border-box;
  border-radius: 12px;
  border: none;
  ${(props) => (props.margin ? `margin: ${props.margin};` : '')};
  cursor: pointer;
  border-color: ${(props) => (props.disabled ? 'gray' : '#ffffff')};
  ${(props) =>
    props.disabled
      ? `background-color:gray; color:white`
      : `
  background-color:#212121; color:white
  `} 
  color:${(props) => props.color}
`;

export default Button;
```

---

**&#128209; reference**

- https://kyounghwan01.github.io/blog/TS/React/styled-components-preset/#%E1%84%8F%E1%85%A5%E1%86%B7%E1%84%91%E1%85%A9%E1%84%82%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3%E1%84%8B%E1%85%A6-%E1%84%89%E1%85%B3%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF-%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC
- https://kyounghwan01.github.io/blog/TS/React/styled-components-preset/
