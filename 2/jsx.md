# JSX

## React에서 JSX를 사용하는 이유

### 앞서 JSX를 먼저 알아보자

- JSX?
  - 자바스크립트의 확장 문법 (Javascript에 XML을 추가한 확장 문법)
  - 공식적인 자바스크립트 문법은 아님
  - 브라우저에서 실행 전 바벨을 사용해 일반 자바스크립트 형태로 변환된다.

### 사용 하는 이유

- 보기 쉽다.
- HTML 태그들을 사용 가능하기에 활용도가 좋다.
- 한 곳에서 모든걸 다 할 수 있다? (HTML,Javascript)

### 특징

- 태그는 반드시 닫혀야한다.
- 최상위 부모 엘리먼트가 있어야한다. 최상위 엘리먼트가 두개이상일 수 없다.

* * *

## 예제

예제를 실행하기 위해 [Babel](https://babeljs.io/repl)로 확인해볼 수 있다. (사용 전 Add Plugin에서 react-jsx를 추가해주어야함)

- 첫번째 예제

```JSX
// JSX 코드
<p>Hello, world!</p>
// 변환된 JS코드
React.createElement("p", null, "Hello, world!");
```

보다시피 jsx에서 HTML 태그인 p태그를 사용하면 변환기가 알아서 js코드로 변환을 시켜준다.

React.createElement라는 함수를 사용한 js코드가 되는것 뿐

거기에 p,null,내용 이 들어가는것

- 두번째 예제

```JSX
// JSX 코드
<Greeting name="world" />
// 변환된 JS코드
React.createElement(Greeting, { name: "world" });
```

React에서 사용하듯 Greeting이라는 함수를 만들고 Greeting을 태그로 사용할 때의 예시인듯하다. 위 경우에는 함수 그 자체를 React.createElement에 바로 넘겨주게 된다.

또한 null이었던 자리에 object의 모습으로 name : "world" 이 들어가는걸 볼 수 있다.

그리고 세번째가 없는걸 볼 수 있는데 여기서 알 수 있듯 세번째는 태그안에 내용이었구나 라는걸 알 수 있다.

- 세번째 예제

```JSX
// JSX 코드
<Button type="submit">Send</Button>
// 변환된 JS코드
React.createElement(Button, { type: "submit" }, "Send");
```

모든게 다 들어가는 예제 코드이다.

여기서 보면 확실히 알 수 있는것같다.

변환된 코드를 보면 첫번째에 태그인 Button이 들어가고, 두번째로 속성값으로 넣어준 type="submit" 이 들어가고, 세번째로는 태그 안에 작성된 Send가 들어가있다.

어떤식으로 변환을 해주는지 확실히 알 수 있는 예제이다.

- 네번째 예제

```JSX
// JSX코드
<div className="test">
 <p>Hello, world!</p>
 <Button type="submit">Send</Button>
</div>

// 변환된 코드
React.createElement(
 "div",
 { className: "test" },
 React.createElement("p", null, "Hello, world!"),
 React.createElement(Button, { type: "submit" }, "Send")
);
```

div라는 태그가 가장 첫번째로 오고 div의 속성인 className이 두번째, 마지막으로 내용으로 들어간 p태그와 Button태그가 세번째로 들어가며 그 안에서 React.createElement가 사용이되어 표현한걸 볼 수 있다.

- 다섯번째 예제

```JSX
// JSX코드
<div>
 <p>Count: {count}!</p>
 <button type="button" onClick={() => setCount(count + 1)}>Increase</button>
</div>
// 반환된 코드
React.createElement(
 "div",
 null,
 React.createElement("p", null, "Count: ", count, "!"),
 React.createElement("button", { type: "button", onClick: () => setCount(count + 1) }, "Increase")
);
```

마지막 예제는 굉장히 복잡하다.

그래도 결국 위 예제들을 이해했다면 충분히 이해할 수 있을듯한 코드다.

다만 count에서 내용 안에 Count:{count}! 인 모습인데 p태그를 변환한 코드를 보며 "Count", count, "!" 이러한 모습으로 처음 보는 형태의 모습인걸 알 수 있다.

* * *

### React Element

- JSX를 사용하지않고 사용할 때 사용한다.

- JSX는 필수가 아니며 JSX없이도 리액트를 사용할 수 있다.

- JSX없이 사용할 땐 React.createElement를 사용하여 트리를 갱신한다.

- 위 예제에서 변환된 코드를 보면 JSX없이 사용할 때 코드를 좀 알 수 있는 것 같다. -

* * *

### VDOM (Virtual DOM)

가상 돔을 알기 전 DOM에 대해서 알면 좋을것 같다.

- DOM (Document Object Model)
  - 웹 또는 웹 앱에 있는 HTML 요소들을 구조적으로 표현한것
  - 자바스크립트를 통해 쉽게 접근하여 조작할 수 있게 해줌
  - 구성요소가 많을수록 느리다.

- VDOM (Virtual DOM)
  - 가상적인 UI의 표현을 메모리에 저장 (재조정)
  - 원하는 최소한의 DOM만 조작할 수 있어서 빠르다.
  - 바뀐 부분만 실제 DOM에 적용한다.

문서를 직접 조작하는건 DOM이라 생각하면 되지않을까? 그에비해

VDOM은 React에서 사용이되는데 가상의 DOM 에서 복제본을 통해 상태를 업데이트 후 업데이트 된 부분만 새롭게 업데이트 시켜주는 리액트의 특징을 뜻하는 것 같다.

React에서 카운트가 업데이트 된다해서 인풋의 내용이 같이 업데이트되어 초기화되는것이 아닌 것을 생각하면 이해가 쉬울 것 같다.

- VDOM은 가상 공간에서 DOM의 복제본을 가지고 업데이트가 일어난 부분만 새롭게 변경시켜주는 것

- 재조정(Reconciliation) - GPT
  - 재조정은 리액트에서 상태가 변경되면 가상돔을 이용해 어느 부분이 변경되야하는지 계산하는 작업이다. 이후 변경된 부분만 실제 DOM에 업데이트 시켜준다.
    1. 변경된 상태를 적용하여 가상 DOM 업데이트
    2. 이전 가상DOM과 새로운 가상 DOM을 비교
    3. 변경된 부분을 찾아서 실제 DOM에 적용

* * *

### React Developer Tools

- StrictMode
  - 개발 모드에서만 활성화 되며 빌드 후 비활성화가 된다.
  - 옛날에 배우기론 평상시보다 엄격하게 버그를 잡아준다.
  - 검색했을 땐 잠재적인 문제를 알아내기 위한 도구로 나온다.

- React Developer Tool
  - 크롬 확장자 도구에서 받아볼 수 있다.
  - 리액트로 개발한 웹의 테스트를 해볼 수 있다.
  - 렌더링 , 로딩시간 등 여러가지 알 수 있다.

* * *

### 리액트에서 VDOM을 사용하는 이유

앞 시간에 배웠듯 리액트의 장점으로 모든걸 리렌더링 하지않고 필요 부분만 렌더링이 가능하다는것이 있다. 이 기능에서 VDOM을 사용하는 것인데 이것이 리액트의 장점이라 생각한다.

모든것이 렌더링되는 불필요한 과정을 버리고 필요 부분만 업데이트 될 수 있도록 해주기위해 VDOM을 사용하는것이다.

* * *

### 나의 생각

리액트에서 JSX를 사용하는 이유로는 좀 더 사용이 편리하기 때문이 아닐까 하고 생각한다. 위 예제 코드에서 많이 느낀거지만 간단한 코드도 JSX를 사용하지않는다면 꽤 번거로울 것 같다 라는 생각을 하게됐다.

VDOM에 대해서는 아주 살짝만 알고있었는데 DOM의 복제본을 가지고 VDOM에서 실행하여 변경사항이 있다면 업데이트를 해준다. 라는 것 까지 자세히 알게된건 처음인 것 같다. 내가 제대로 이해한 것 인지는 잘 모르겠지만 지금은 그렇다.
