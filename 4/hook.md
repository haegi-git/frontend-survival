# 리액트의 Hook

## 학습 키워드

* React Hook 이란
* Hooks
  * useState
  * useEffect
  * useContext
  * useRef
  * useLayoutEffect
* React StrictMode 란

* * *

### React Hook 이란

[hook을 사용하는 이유](https://hyeon-joo.tistory.com/2)

React 16.8에서 부터 Hooks가 도입이되었다. 기존 몇가지 방식에 있던 몇 문제를 해결

기존 방식의 문제점

* Wrapper Hell (Hoc) : Hooks 이전에 HOC(Higher Order Component)를 이용하여 코드를 반복해서 작성하는 문제를 해결하려 했었다. HOC란 화면에서 재사용 가능한 로직만 분리하여 component로 만들고 재사용 불가능한 부분은 parameter로 받아 처리하도록 하는 패턴이다.
  * 여기서 HOC를 Wrapper Hell이라 하는 이유는 중첩되는 컴포넌트가 많아져 depth가 깊어지는 것을 의미함
* Huge Components
* Confusing Classes

Hooks가 나오며 React를 사용하는 방식에 변화가 많이 생겨났다.

과거의 리액트는 경험해보지 못하여서 실감은 못할 것 같다.

Hook은 로직 분리가 가능하며 위 문제점에 Wrapper Hells를 피하고 리액트 component life cycle에 종속적이지 않도록 해준다.

Hook으로 인해 요즘의 리액트는

* Function Component만 사용하며
* 상태 관리 유무를 바로 알기 어려움 = 신경쓰지않아도된다.
* 복잡한 요소는 전부 Hook으로 격리 및 재사용 가능하다.

대표적인 Hooks들로

* useState -> State Hook -> React의 state
* useEffect -> Side-effect
* useContext
* useRef
* useLayoutEffect -> useEffect와 조금 다르다.

등이 있는데 useState와 useEffect는 자주 사용해봤었다.

use가 붙은 친구들은 대부분 hook으로 이해해도된다.

* * *

### Hooks

* useState

useState Hook은 React에서 상태를 관리하기위한 메서드다.

앞 시간에서도 몇차례 나왔으며 간단히 생각하면 값이 변경될 변수라 생각해도 될듯하다.

* useEffect

useEffect는 side effect를 수행하기위한 메서드이다.

useEffect는 내가 알고있는 지식으로는 렌더링의 과정마다 훅을 걸어주는 도구이다.

useEffect를 사용하면 마운트 될 때, 업데이트 될 때 마다, 언마운트 될 때를 관리할 수 있다.

마운트는 화면에 나타났을 때

언마운트는 화면에서 사라질 때

업데이트는 특정 props가 변경될 때

```js
useEffect(()=>{
    console.log('마운트 됐다');
    return()=>{
        console.log('언마운트 됐다');
    }
},[])
```

useEffect에 콤마 뒤 괄호[]는 디펜던시 어레이로 특정 요소가 업데이트 될 때 useEffect를 관리해줄 수 있음

타이머 예시

```js
function Timer() {
 useEffect(() => {
  setInterval(() => {
   document.title = `Now: ${new Date().getTime()}`;
  }, 100);
 });

 return (
  <p>Playing</p>
 );
}

export default function TimerControl() {
 const [playing, setPlaying] = useState(false);
 
 const handleClick = () => {
  setPlaying(!playing);
 };

 return (
  <div>
   {playing ? (
    <Timer />
   ) : (
    <p>Stop</p>
   )}
   <button type="button" onClick={handleClick}>
    Toggle
   </button>
  </div>
 );
}
```

위 코드는 당연히 토글버튼이 정상작동하지않는다.
토글 버튼으로 Timer 컴포넌트를 제어하는중이지만 첫 실행은 제대로 작동하지만 멈추는 기능까지는 작동하지않는다.

```js
useEffect(() => {
 const savedTitle = document.title;

 const id = setInterval(() => {
  document.title = `Now: ${new Date().getTime()}`;
 }, 100);

 return () => {
  document.title = savedTitle;
  clearInterval(id);
 };
});
```

멈추는 기능이 작동하지않는걸 고쳐주기위해 언마운트 부분에 멈추는 기능을 추가해주면 된다.

언마운트에 clearInterval은 interval 타이머를 해제해주는 메서드이다.

최종적으로 작동되는 모양은

1. 토글 버튼을 첫 클릭 시 마운트(Timer 컴포넌트가 생성)
2. 토글 버튼을 두번 째 클릭 시 언마운트(Timer 컴포넌트가 사라짐)
3. 언마운트는 컴포넌트가 사라지면서 작동하는 부분이기에 interval 타이머를 해제하며 타이머가 멈추게됨

디펜던시 어레이의 예시

```js

function Timer() {
 useEffect(() => {
  setInterval(() => {
   document.title = `Now: ${new Date().getTime()}`;
  }, 100);
 });

 return (
  <p>Playing</p>
 );
}

export default function TimerControl() {
 const [playing, setPlaying] = useState(false);
 const [count,setCount] = useState(0);

 useEffect(()=>{
    console.log('Effect');
 })
 
 const handleClick = () => {
  setPlaying(!playing);
 };


 return (
  <div>
   {playing ? (
    <Timer />
   ) : (
    <p>Stop</p>
   )}
   <button type="button" onClick={handleClick}>
    Toggle
   </button>
   <p>{count}</p>
   <button type="button" onClick={() => setCount(count + 1)}>
    Increase
   </button>
  </div>
 );
}
```

위 코드는 디펜던시 어레이를 사용하지 않았을 때 클릭시 숫자가 하나씩 증가하는 버튼을 만들었을 때 콘솔창에 계속해서 effect가 찍히는걸 볼 수 있을것이다. 디펜던시 어레이를 사용한다면 그러한 불필요한 동작을 막아줄 수 있다.

```js

function Timer() {
 useEffect(() => {
  setInterval(() => {
   document.title = `Now: ${new Date().getTime()}`;
  }, 100);
 });

 return (
  <p>Playing</p>
 );
}

export default function TimerControl() {
 const [playing, setPlaying] = useState(false);
 const [count,setCount] = useState(0);

 useEffect(()=>{
    console.log('Effect');
 },[playing])
 
 const handleClick = () => {
  setPlaying(!playing);
 };


 return (
  <div>
   {playing ? (
    <Timer />
   ) : (
    <p>Stop</p>
   )}
   <button type="button" onClick={handleClick}>
    Toggle
   </button>
   <p>{count}</p>
   <button type="button" onClick={() => setCount(count + 1)}>
    Increase
   </button>
  </div>
 );
}
```

위 코드는 디펜던시 어레이에 playing을 추가해주어 playing이 변경될 때만 콘솔창에 Effect를 찍는 동작을 할 수 있다.

이렇게 디펜던시 어레이 의존성 배열을 사용하게되면 불필요한 업데이트를 막아줄 수 있게된다.

또한 딱 한번만 실행되게끔 하고싶다면 디펜던시 어레이를 빈 배열로 넣어주면 한번만 실행되게끔 할 수 있다.

한번만 실행되게끔 사용할 땐 데이터를 받아올 코드를 사용해줄 때 사용하게되는것같다. 데이터는 한번만 불러오면 끝이니까

그리고 useEffect부분이 콘솔에 두번씩 출력되는건 StrictMode 때문이다. 많이 신경쓰인다면 StrictMode를 빼두어도됨

[디펜던시 어레이로 Fetch할때 주의점](https://react.dev/learn/synchronizing-with-effects#fetching-data)

* useRef

[참고 자료](https://velog.io/@jinyoung985/React-useRef%EB%9E%80)

[공식 문서]()

useRef는 저장공간 또는 DOM 요소에 접근하기 위해 사용되는 React Hook이다. 여기서 ref는 reference, 참조를 뜻하며

useRef는 컴포넌트의 생애주기를 통해 유지가 되며 생애주기는 마운트와 언마운트를 뜻하고 .current 프로퍼티로 변경 가능한 ref 객체를 반환해준다.

```js
const ref = {
  value : 1;
}
```

ref를 사용하는 여러 컴포넌트가 존재한다 가정하에 위 같이 useRef를 사용하지않고 const ref 에 객체로 value가 존재할 때

ref를 사용하는 컴포넌트가 12개라면 어느곳에서

```js
ref.value += 1;
```

이러한 코드가 존재한다면 + 1이 되는것이아닌 12가 더해지는 상황이 생긴다. 그런 상황을 막아주며 여러곳에서도 제어가 가능한 것 같다.

useRef를 사용하는것과 useState를 사용하는것에 별 차이를 못느끼고 별 차이가없어 useState를 사용해도 될 것 같지만

useState는 상태가 변경이되면 해당 컴포넌트와 하위 컴포넌트가 재렌더링되지만

useRef는 값(current)이 바뀌어도 렌더링에 영향을 주지는않는다.

```js
const counter = useRef(0);

const handelClick = () =>{
  counter.current += 1;
}

return(
  <div>
  <p>{counter.current}</p>
  <button onClick={handelClick}>상승</button>
  </div>
)
```

위와 같이 counter에 useRef로 0을 잡아준 뒤 화면에 띄워준 다음

버튼을 누르면 counter의 숫자가 1씩 더해지는 버튼을 만들었을 때 누를 때 마다 counter는 증가하고는 있겠지만 화면은 재렌더링이 일어나지않기에 p태그 안에 띄워준 값은 실시간으로 변경되지 않을 것이다.

### 실시간 렌더도 안되는데 왜 사용하는지?

주요 용도로

1. 컴포넌트가 사라질 때까지 동일한 값을 써야할 경우, input 등의 ID관리
2. (useEffect 등과 함께 쓰면서 만나게 되는) 비동기 상황에서 현재 값을 제대로 쓰고 싶은 경우

Closure → 변수를 capture, bind를 깜빡하는 문제가 종종 일어남.

이라고 하는데 아직까지는 완벽히 이해가 되진않는다.

useRef를 이해하기위해선 사용을 해보며 이해를 해야할 것 같다.

* useContext

[참고 자료](https://www.zerocho.com/category/React/post/5fa63fc6301d080004c4e32b)

useContext는 쉽게 설명하면 props를 글로벌하게 사용하게 해준다.

여태 A에 있던 데이터를 B로 넘겨주기위해 Props를 사용해 넘겨주었다면

만약 A에 있는 데이터를 B > C > D > E ... G까지 넘겨주려면?

B와 C > D E ... 모든 컴포넌트를 거쳐서 건너주어야한다.

그러한 귀찮고 번거로운 코드를 useContext를 사용하면 한번에 넘겨줄 수 있다.

비슷한 걸로 Redux가 존재한다.

* useLayoutEffect

[참고 자료](https://www.howdy-mj.me/react/useEffect-and-useLayoutEffect)

처음 들어보는 Hook이었다.

검색을 해보니 useEffect와 비슷하나 차이가 있는것같다.

useEffect로 전달된 함수는 layout과 paint가 완료된 후 비동기적으로 실행이되고

useLayoutEffect는 useEffect와 동일하나 렌더링 후 layout과 paint 전에 동기적으로 실행이 된다.

* * *

### React StrictMode란?

[참고 자료](https://zereight.tistory.com/587)

React StrictMode란 간단히 이해하자면 개발을 하는 사용자를 돕기위한 도구이다.

StrictMode를 사용하면 잠재적인 문제를 알아낼 수 있고 Fragment와 같이 UI를 렌더링 하지 않으며 자손들에 대한 부가적인 검사와 경고를 활성화 해준다.

* * *

이번 정리의 주요 핵심은 Hook이며 useState와 useEffect, useRef를 중심으로 이해하려 노력을 해주면 좋을 것 같다.

사실 useState와 useEffect에 대해서는 이미 알고있기도하고 사용 경험도 얼추 있기에 이해하는데 쉬웠지만 useRef는 사용해본 경험은 있지만 아직도 잘은 모르겠다. 사용해보며 더 이해를 해보도록 해야겠다.