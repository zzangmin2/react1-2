# 김정민 202230107

## 4월 3일 강의

### 1.Props 사용법

- JSX에서는 Key-value 쌍으로 props 구성
- JSX는 중괄호를 사용하면 JS코드를 넣을 수 있음
- JSX를 사용하지 않는 경우 props 전달 방법은 createElement()함수를 사용하는 것

### 2 컴포넌트 만들기

1. 컴포넌트 종류

- 리액트 초기 버전을 사용할 때는 클래스형 컴포넌트를 주로 사용했음
- 이후 Hook 기능이 좋아지면서 최근에는 함수형 컴포넌트 사용

- 함수형 컴포넌트
  ```js
  funciton welcome(){
    return <h1>안녕</h1>
  }
  ```
- 클래스형 컴포넌트

```js
class Welcome extends React.Components {
  render() {
    return <h1>안녕</h1>;
  }
}
```

2. 컴포넌트 이름 짓기

- 항상 대문자로 시작 ( 소문자로 시작하는 컴포넌트를 DOM 태그로 인식)
- 컴포넌트 파일 이름과 컴포넌트 이름은 같게

3. 컴포넌트의 렌더링

```js
const element = <Welcome name="길동" />;
ReactDOM.render(
  element,
  document.getElementById("root");
)
```

4. 컴포넌트 합성

- 여러개의 컴포넌트를 합쳐서 하나의 컴포넌트를 만드는 것

  ```js
  return (
    <div>
      <Welcome name="aaa" />
      <Welcome name="bbb" />
      <Welcome name="ccc" />
      <Welcome name="dddd" />
    </div>
  );
  ```

5. 컴포넌트 추출

- 큰 컴포넌트에서 일부를 추출해서 새로운 컴포넌트를 만드는 것

**기본적으로 하나의 컴포넌트에서는 하나의 역할을 수행하도록 하는 것이 바람직**

### 3.1 state

1. state?

- 리액트 컴포넌트의 상태
- 상태는 컴포넌트의 데이터를 의미. 즉 변경가능한 데이터를 의미
- state가 변하면 다시 렌더링 되기 때문에 렌더링과 관련된 값만 state에 포함시켜야 함

2. state의 특징

- 리액트만의 특별한 형태가 아니고 단지 자바스크립트 객체임
- state는 변경은 가능하지만 직접 수정이 안됨
- state를 변경하고자 할 때는 set함수를 사용

### 3.2 생명주기

- 생명주기는 컴포넌트의 생성 시점, 사용 시점, 종료 시점을 나타냄
- constructor가 실행 되면서 컴포넌트 생성
- 컴포넌트가 소멸하기 전까지 여러번 렌더링



## 3월 27일 강의

### 1.1 JSX의 역할

- JSX는 내부적으로 XML/HTML 코드를 자바스크립트로 변환
- react가 createElement함수를 사용햐여 자동으로 자바스크립트로 변환

- JSX는 코드가 간결해지고 가독성이 향상됨

```js
//JSX 사용
ReactDOM.render(<Hello toWhat="World" />), document.getElementById("root");

//JS 그대로 사용
ReactDOM.render(
  React.createElement(Hello, { toWhat: "World" }, null),
  document.getElementById("root")
);
```

### 1.2 JSX의 사용법

- 모든 자바스크립트 문법을 지원한다.
- 자바스크립트 문법에 XML과 HTML을 섞어서 사용

```js
const element = <img src={user.avatarUrl}></img>;
```

### 2.1 엘리먼트 정의

- <b>엘리먼트는 리액트 앱의 가장 작은 빌딩 블록들</b>
- 엘리먼트는 리액트 앱을 구성하는 요소를 의미
- 웹사이트의 경우는 DOM 엘리먼트이며, HTML요소를 의미

<b>리액트 엘리먼트 vs DOM 엘리먼트</b>

- 리액트 엘리먼트: Virtual DOM 형태. 리액트 엘리먼트는 변화한 부분만 가지고 있어 가벼움.
- DOM 엘리먼트: 페이지의 모든 정보를 가지고 있어 무거움.

### 2.2 엘리먼트 생김새

- 자바스크립트 객체의 형태로 존재
- 컴포넌트, 속성 및 내부의 모든 children을 포함하는 일반 JSX객체
- 객체는 불변성을 가지고 있음

- 내부적으로 자바스크립트 객체를 만드는 함수 -> createElement()

### 2.3 엘리먼트 특징

- 리액트 엘리먼트의 가장 큰 특징은 <b>불변성</b>
- 만약 내용이 바뀌면?
  - 컴포넌트를 통해 새로운 엘리먼트를 생성
  - 교체하는 작업을 위해 virtual DOM사용

### 2.4 엘리먼트 렌더링하기

- Root DOM node
  - `<div id="root"></div>` -> 태그 안에 엘리먼트가 렌더링 되면 이것을 Root DOM node라고 함.
  - `ReactDOM.render(element, document.getElementById('root'))` -> render()함수를 사용해서 엘리먼트를 렌더링. 첫 번째 파라미터는 출력할 리액트 엘리먼트이고, 두번 째 파라미터는 출력할 타겟을 나타냄

### 3.1 컴포넌트에 대해 알아보기

- 컴포넌트 구조라는 것은 작은 컴포넌트가 모여 큰 컴포넌트를 구성하고, 다시 이런 컴포넌트들이 모여서 전체 페이지를 구성하는 것을 의미
- 컴포넌트는 재사용이 가능하기 때문에 개발 시간과 유지 보수 비용도 줄일 수 있음
- 컴포넌트는 자바스크립트 함수와 입력과 출력이 있다는 면에서는 유사
- 입력은 Props가 담당하고, 출력은 리액트 엘리먼트의 형태로 출력
- 엘리먼트를 필요한 만큼 만들어 사용한다는 면에서 객체지향의 개념과 비슷함

### 3.2 Props

1. 개념

   - property의 준말
   - props가 바로 컴포넌트의 속성
   - props에 따라 속성이 다른 엘리먼트 출력

2. 특징

   - 읽기 전용. 즉 변경할 수 없음
   - 속성이 다른 엘리먼트를 생성하려면 새로운 props를 컴포넌트에 전달

**Pure 함수 vs Impure 함수**

- pure 함수는 인수로 받은 정보가 내부에서도 변하지 않는 함수<br>
  `function sum (a , b ){ return a + b }`
- Impure 함수는 인수로 받은 정보가 내부에서 변한느 함수<br>
  `function withdraw(account, amount){ return account.total -= amount }`

- **모든 리액트 컴포넌트는 그들의 Props에 관해서는 Pure 함수 역할을 함**

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
