# 김정민 202230107

## 5월 22일 강의

### 1. 리스트와 키

- 리스트는 자바스크립트의 변수나 객체를 하나의 변수로 묶어 놓은 배열과 같은 것
- 키는 각 객체나 아이템을 구분할 수 있는 고유한 값
- 리액트에서는 배열과 키를 사용하는 반복되는 다수의 엘리먼트를 쉽게 렌더링
- 키는 리스트에서 어떤 아이템이 변경, 추가 또는 제거되었는지 구분하기 위해 사용
- 키는 같은 리스트에 있는 엘리먼트 사이에서만 고유한 값이면 됨

- 제어 컴포넌트는 사용자가 입력한 값에 접근하고 제어할 수 있도록 해주는 컴포넌트

- _map함수 사용하기_

```js
{
  students.map((student) => {
    return <li key={student.id}>{student.name}</li>;
  });
}
```

## 5월 8일 강의

### 1. Arguments 전달하기

- 함수를 정의할 때는 parameter 혹은 매개변수, 함수를 사용할 때는 argument 혹은 인수라고 부름

```js
<button onClick={(event)=> this.deleteItem(id, event)}>삭제하기</button>
<button onClick={this.deleteItem.bind(this, id)}>삭제하기</button>
```

### 2. 엘리먼트 변수

- 렌더링해야 될 컴포넌트를 변수처럼 사용하는 방법이 엘리먼트 변수

```js
let button = <LogoutButton onClick={handleLogoutClick}>
```

### 3. 인라인 조건

- 필요한 곳에 조건문을 직접 넣어 사용하는 방법

- 1. 인라인 if

  - if문을 직접 사용하지 않고, 동일한 효과를 내기 위해 && 논리연산자를 사용
  - &&는 and 연산자로 모든 조건이 참일 때만 참이 됨.
  - 첫 번째 조건이 거짓이면 두 번쨰 조건은 판단할 필요가 없음

  ```js
  {
    count && <h1>현재 카운트: {count}</h1>;
  }
  ```

- 2. 인라인 if-else

  - 삼항 연산자를 사용함

  ```js
  {
    isLoggedIn ? <LogoutButton /> : <LoginButton />;
  }
  ```

### 4. 컴포넌트 렌더링 막기

- 컴포넌트를 렌더링 하고 싶지 않을 떄는 null 리턴

## 5월 1일 강의

### 1. 훅의 규칙

- _훅의 두 가지 규칙_
- 첫 번째 규칙은 무조건 최상위 레벨에서만 호출해야한다는 것
- 따라서 반복문이나 조건문 또는 중첩된 함수들 안에서는 훅을 호출하면 안 됨
- 이 규칙에 따라서 훅은 컴포넌트가 렌더링 될 떄마다 같은 순서로 호출되어야 함

- 두 번째 규칙은 함수형 컴포넌트에서만 훅을 호출해야함
- 따라서 일반 자바스크립트 함쉥서 훅을 호출하면 안 됨
- 훅은 함수형 컴포넌트 혹은 직접 만든 커스텀 훅에서만 호출할 수 있음

### 2. 나만의 훅 만들기

- 이름은 use로 시작해야함. 그렇지 않으면 다른 훅을 불러 올 수 있음

```js
import { useState, useEffect } from "react";

export default function UserStatus(userId) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ServerAPI.subscribeUserStatus(userId, handleStatusChange);
    return () => {
      ServerAPI.unsubscribeUserStatus(userId, handleStatusChange);
    };
  });

  return isOnline;
}
```

### 3. 이벤트 처리하기

- DOM에서 클릭 이벤트를 처리하는 코드와 React에서 클릭 이벤트를 처리하는 코드의 차이 점

1. 이벤트 이름이 onclick (DOM), onClick(React)
2. 전달하려는 함수는 문자열 (DOM), 함수 그대로(React)

- 이벤트가 발생했을 떄 해당 이벤트를 처리하는 함수를 이벤트 핸들러라고 함
- 이벤트가 계속 발생하는 것을 계속 듣고 있다는 의미로 이벤트 리스너라고 부르기도 함

## 4월 17일 강의

### 1. 훅?

- 클래스형 컴포넌트에서는 생성자에서 state를 정의하고, setState()함수를 통해 state를 업데이트 함
- 예전에 사용하던 함수형 컴포넌트는 별도로 state를 정의하거나, 컴포넌트의 생명주기에 맞춰서 어떤 코드가 실행되도록 할 수 없었음
- 함수형 컴포넌트에서도 state나 생명주기 함수의 기능을 사용해주기 위해 추가된 기능 -> 훅(hook)
- 훅(hook)이란?
  - state와 생명주기 기능에 갈고리를 걸어 원하는 시점에 정해진 함수를 실행되도록 만든 함수
  - 훅의 이름은 모두 use로 시작
  - 사용자 정의 훅을 만들 수 있음.

### 2. useState

- 함수형 컴포넌트에서 state를 사용하기 위한 hook

```js
export default function Counter(props) {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>총 {count}</p>
      <button onClick={() => setCount(count + 1)}>클릭</button>
    </>
  );
}
```

### 3. useEffect

- 사이드 이펙트를 수행하기 위한 것
- 서버에서 데이터를 받아오거나 수동으로 DOM을 변경하는등의 작업을 수행해야하는 것과 같이 다른 컴포넌트에 영향을 미칠 수 있는 작업은 렌더링 중에 작업이 완료될 수 없음 -> 렌더링이 끝난 이후에 실행되어야 함
- 클래스 컴포넌트의 생명주기 함수와 같은 기능을 하나로 통합한 기능을 제공

```js
useEffect(() => {
  document.title = `총 ${count}번 클릭했습니다`;
}, [count]);
```

### 4. useMemo

- Memoized value를 리턴하는 함수
- 이전 계산 값을 갖고 있기 때문에 연산량이 많은 작업의 반복을 피할 수 있음
- 렌더링이 일어나는 동안 실행

- 메모이제이션(memoiztion)?
  - 컴퓨터 프로그램이 동일한 계산을 반복해야할 떄, 이전에 계산한 값은 메모리에 저장함으로써 동일한 계산의 반복수행을 제거하여 프로그램 실행속도를 빠르게 하는 기술. 동적 계획법의 핵심이 되는 기술

### 5. useCallback

- useMemo()와 유사한 역할

### 6. useRef

- 레퍼런스를 사용하기 위한 훅
- 레퍼런스란 특정 컴포넌트에 접근할 수 있는 객체를 의미
- 레퍼런스 객체에는 .current라는 속성이 있는데, 이것은 현재 참조하고 있는 엘리먼트를 의미
- 이렇게 반환된 레퍼런스 객체는 컴포넌트의 라이프타임 전체에 걸쳐 유지
- 즉, 컴포넌트가 마운트 해제 전까지는 계속 유지 됨

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
