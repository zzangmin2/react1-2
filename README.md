# 김정민 202230107

## 3월 20일 강의

### 1.1 리액트의 정의

- ~~사용자 인터페이스를 만들기 위한 자바스크립트 라이브러리~~
- <b>웹 및 앱 유저 인터페이스를 위한 라이브러리</b>

- 복잡한 사이트를 쉽고 빠르게 만들고, 관리하기 위해 만들어진 것이 바로 리액트
- 다른 표현으로는 SPA를 쉽고 빠르게 만들 수 있는 도구

### 1.2 리액트의 장점

1. 빠른 업데이트와 렌더링 속도

- DOM( Document object model)
- virtual DOM: DOM 조작이 비효율 적인 이유로 속도가 느리기 때문에 고안된 방법
- DOM : 동기식, virtualDOM: 비동기식

### 2. 컴포넌트 기반 구조

- 리액트의 모든 페이지는 컴포넌트로 구성
- 하나의 컴포넌트는 다른 여러 개의 컴포넌트의 조합으로 구성이 되어 재사용성이 뛰어남

### 3. 재사용성

- 반복적인 작업을 줄여주기 떄문에 생산성을 높여 주고 유지보수가 용이
- 단, 모듈의 의존성이 없어야 함

#### CDN(Content Delivery Network)?

- 전 세계에 분산된 서버 네트워크를 이용하여 사용자에게 웹 콘텐츠를 더 빠르게 제공하는 시스템

### 리액트 시작하기

```
npx create-react-app 프로젝트이름
```

### 리액트의 메인 컴포넌트

App.js

```js
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```

index.js

```js
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### package.json ? package-lock.json
- 패키지 의존성 관리 파일
- package-lock.json은 package.json이 변경될 떄마다 업데이트 되는 것으로 좀 더 정확한 버전이 기록되어있음

## 3월 13일 강의

- 1. HTML
- 2. CSS
- 3. JavaScript (SPA)

  - Function statement
    ```js
    function a() {}
    ```
  - Arrow function expression
    ```js
    const function =()=>{}
    ```

- 4. node
  - npm(node package manager)
  - npx(node)
