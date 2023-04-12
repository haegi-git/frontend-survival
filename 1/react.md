## React

### 학습 키워드

* React란?
* React 컴포넌트
* React 리렌더링
* IoC(Inversion of Control)
* Library vs Framework

***

### React란?

[React 공식 문서](https://ko.reactjs.org/)   
[React Beta 문서](https://react.dev/)   
리액트가 무엇인지 알고싶을 때 참고할 것

### React 컴포넌트

* 리액트에서 화면 UI 요소를 구분할 때 사용한다고 한다.
* 컴포넌트에는 함수형 컴포넌트, 클래스형 컴포넌트가 있다.
    * 함수형 컴포넌트를 주로 사용한다.

### React 렌더링

```
function Greeting() {
  return (
    <p>Hello, world!</p>
  );
}

function main() {
  const element = document.getElementById('root');

  if (!element) {
    return;
  }

  const root = ReactDOM.createRoot(element);

  root.render(<Greeting />);
}

main();
```

* 여러 Root를 만들거나 여러번 render해도 된다.
* React는 여러번 render해도 변경된 부분만 업데이트가 되기에 다른곳은 그대로 유지되는걸 볼 수 있다.   

[변경된 부분만 업데이트되는 예제](https://react.dev/reference/react-dom/client/createRoot#updating-a-root-component)

위 예제를 보면 알 수 있듯 초당 변경되는 count만 업데이트가 이루어지고 인풋의 글씨는 계속 유지가 되는걸 볼 수 있다.

### React 리렌더링

[언제 리렌더링이 되느냐?](https://velog.io/@surim014/react-rerender)   
[왜 리액트에서 리렌더링이 발생하느냐](https://medium.com/@yujso66/%EB%B2%88%EC%97%AD-%EC%99%9C-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EB%A6%AC%EB%A0%8C%EB%8D%94%EB%A7%81%EC%9D%B4-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94%EA%B0%80-74dd239b0063)   
[리액트 렌더링에 대한 거의 완벽한 가이드](https://velog.io/@superlipbalm/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior)   

* Props 또는 State가 변경이 될 때 리렌더링이 된다.
* 부모 컴포넌트가 리렌더링이 되면 속해 있는 자식컴포넌트도 리렌더링이 된다.

### IoC (Inversion of Control)

* 사실 이건 처음 들어보는 단어이다.
* 제어의 역전 이라고 하며 프레임워크의 주요한 특징이다.
* React는 IoC를 통해 상태와 업데이ㅡ가 얽힌 복잡한 상황을 간단히 선언형 UI로 구성하는 혜택을 누린다.
    * IoC에 대해서는 궁금하다면 따로 더 찾아봐야할 듯

### 리액트는 라이브러리냐 프레임워크냐

면접에서 자주 나오는 단골 질문이고 나 또한 이 질문에 대해   
알아본 적이 있었다.   

[React개발자의 답변](https://twitter.com/trueadm/status/1194567962784653312)   

둘 다 라고 알려준다. 누구는 라이브러리다 누구는 프레임워크다 라고 말이많기에 자세히 알고자 하면 따로 알아보면 좋을듯하다.