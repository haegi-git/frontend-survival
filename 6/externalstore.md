# External Store

## 학습 키워드

* 관심사의 분리
* Layered Architecture
* Flux Architecture
* useReducer
* useCallback

* * *

### 관심사의 분리

[참고 자료](https://sylagape1231.tistory.com/111)

관심사의 분리라는 것은 소프트웨어 개발에서 가장 기본적인 원칙 중 하나로 SOLID 원칙 중 2개(단일 책임 원칙 및 인터페이스 분리)가 이 개념에서 파생될 정도로 매우 중요하다.

리액트를 여태 사용하면서 여러 컴포넌트 작은 컴포넌트들을 하나씩 모아서 큰 컴포넌트 하나를 구성하는 것도 비슷한 개념이다.

App 안에 헤더 메인 푸터가 존재하고 메인안에 다른 Counter Posts 등이 존재하고 그 안에 또 다른 컴포넌트가 존재하고 ...

그런식으로 각각의 컴포넌트들은 서로 다른 관심사를 가지고있다.(기능이 다르다.)

* 관심사의 분리로 복잡한 코드를 비슷한 기능을 하는 코드들 끼리 별도로 관리하는 것
* 컴포넌트 별로 관심사를 분리하면 확장성과 재사용성이 높아진다.

### 리액트에서 컴포넌트를 분리하는 이유?

* 어떠한 컴포넌트는 UI를 표현할 수 있고 어떠한 컴포넌트는 동작하는 로직을 기능을 담아둘 수 있다.
* 또한 UI와 기능 모두 담아두는 컴포넌트도 존재할 수 있고 하나도 담지않는 컴포넌트도 존재할 수 있다.
* 컴포넌트는 재사용할 수 있는 최소 UI 단위임에도 불구하고 컴포넌트에서 수행하려는 역할에 따라 얼마든지 복잡해질 수 있다.

### 리액트에서 컴포넌트를 분리하는 기준

* 공식 문서 기준
  * UI 일부가 여러번 사용되거나 UI 일부가 자체적으로 복잡한 경우 분리하는 것이 좋다.
* UI로 기준을 잡는 것 외에 프로젝트마다 기준점을 어디에 잡는지에 따라 컴포넌트 분리 기준이 존재한다.
  * View와 로직을 분리 또는 State에 따라 분리 등등
* 프로젝트에 적용하기 용이한 적절한 컴포넌트 분리 예시
  * 해당 컴포넌트가 너무 길어서 가독성이 떨어지지 않는지
  * 다른 컴포넌트에서 재사용될 수 있는지

### 컴포넌트 분리 과정

* 재사용하고자 하는 컴포넌트의 UI를 보며 그 중 동일한 요소가 무엇인지, 다른 요소는 무엇인지 파악한다
* 다른 요소를 데이터로 구성
* 해당 데이터를 하나의 컴포넌트에서 필요한 곳에 사용

컴포넌트를 잘 나누어놓는다면 단위테스트에도 좋다.

* * *

### Layered Architecture

[참고 자료](https://devmoony.tistory.com/178)

계층화 아키텍처란 아키텍처의 컴포넌트들은 각각 어플리케이션의 특정한 역할을 수행하도록 가로로 나누어져 계층을 이루며 가장 널리 알려진 아키텍처로 전통적인 IT workflow와 조직 구성이 잘 맞아 떨어져 비즈니스에서 채택되며 주로 3계층으로 이루어져있다.

* 프레젠테이션 레이어
  * 이 계층은 클라이언트의 요청을 받고 응답하는 계층이다. 이 계층의 특징은 어떻게 클라이언트의 요청을 처리할 것인지는 관심이 없고 그저 어떻게 받고 응답을 어떻게 할지에 대해 관심이 있는 계층이다.
* 비즈니스 레이어
  * 비즈니스 로직을 담당하는 계층으로 프레젠테이션 레이어가 클라이언트의 요청을 받아오면 비즈니스는 실제 요청에 대한 처리를 하는 부분이다.
* 퍼시스턴스 레이어
  * 데이터 베이스에 접근하는 계층으로 비즈니스의 요청 처리에 따라 데이터베이스에서 데이터를 저장, 조회, 삭제 등의 로직을 수행한다.
* 데이터베이스 레이어
  * 말 그대로 데이터베이스 그 자체

### 레이어드 아키텍처의 핵심 요소

계층화 아키텍처의 핵심 요소는 단방향 의존성이다. 각각의 레이어는 오직 자기보다 하위에 있는 레이어에만 의존한다. 그러므로 프레젠테이션 레이어는 비즈니스 레이어에 의존하고 비즈니스 레이어는 퍼시스턴스 레이어에게만 의존한다. 또 다른 핵심 요소로는 각 레이어의 역할이 명확하다. 라는 것이다.

* * *

### Flux Architecture

[참고 자료](https://velog.io/@alskt0419/FLUX-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90%EB%9E%80)

플럭스 아키텍처를 알기전 MVC 아키텍처에 대해 알아야 하는 듯 하다.

플럭스 아키텍처는 페이스북에서 개발한 단방향 데이터 흐름을 가지는 아키텍처이다.

MVC아키텍처의 구조
![MVC아키텍처 구조](https://velog.velcdn.com/images%2Falskt0419%2Fpost%2Fee1b0474-26a8-448e-bc2f-cda1724038fa%2Fimage.png)

위와 같은 구조를 가지는데 Controller는 Model의 데이터를 조회 하거나 업데이트하는 역할을 하고 Model은 이런 데이터를 View 통해 반영시킨다. 또 View는 사용자로부터 데이터를 입력받기도하며 때문에 사용자의 입력이 Model에 영향을 주기도 한다.

문제는 이러한 구조가 거대한 어플리케이션을 대상으로 한 프로젝트에서는 너무 복잡하고 빨라진다는 것

페이스북에서 얘기한 구조의 복잡성
![구조의 복잡성](https://velog.velcdn.com/images%2Falskt0419%2Fpost%2F35a7a12e-4f0d-416c-889c-92bdeca47dbb%2Fimage%20(1).png)

### MVC의 문제점

사용자와의 상호작용이 View에서 일어나기에 사용자의 입력에 따라 Model을 업데이트 해줘야하는 경우가 있고 여기서 의존성의 이유로 하나의 모델만이 아닌 다른 모델까지 업데이트 해줘야하는 경우도 생김

그 외에도 가끔 이러한 문제 때문에 아주 많은 변경을 초래하는 경우도 있었음

### 해결 방안으로 나온 것이 단방향 데이터 흐름

단방향 데이터 흐름을 가지는 구조는 데이터는 단방향으로 흐르며 새로운 데이터를 넣게되면 처음 부터 다시 시작되는 방식으로 설계 되어있다. 이러한 시스템 구성을 플럭스 구조라 불렀다.

### 플럭스 구조?

![플럭스 구조](https://velog.velcdn.com/images%2Falskt0419%2Fpost%2F368e2aec-aa71-45fd-9359-8781ba90290b%2F%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C.png)

플럭스의 시스템 구조의 가장 큰 특징은 단방향 데이터 흐름이다.

데이터의 흐름은 디스패처 -> 스토어 -> 뷰 순이며 뷰에서 입력이 발생하면 액션을 통해 디스패쳐로 향하게 된다.

* Dispatcher(디스패쳐)
  * 디스패쳐는 플럭스 어플리케이션의 모든 데이터 흐름을 관리하는 일종의 허브 역할을 한다. 액션이 발생하면 디스패처로 메세지나 액션 객체나 전달되고 디스패쳐에선 이러한 메세지 혹은 액션객체를 콜백 함수를 통해 스토어로 전달해준다. 스토어에 접근하기 위한 일종의 단계이며 액션을 통해 스토어에 접근하기 위해서는 디스패처의 단계를 거쳐야 한다.
* Action(액션)
  * 디스패쳐를 통해 스토어에 변화를 일으킬 수 있는데 이때 디스패쳐의 데이터 묶음을 액션이라한다. 예를 들어 GET_POST라는 게시글을 가져와 스토어의 상태값을 변경해 주는 함수를 실행하고 싶을 때는 GET_POST라는 이름의 액션을 발생 시키는 것 아래에 payload 값을 넣어 데이터를 관리할 수 있다. 예시는 리덕스, 나의 경우는 리덕스 툴킷을 사용했었다.
  
```js
dispatch({ <= 디스패쳐
 type: GET_POST, <= 액션 이름
    // GET_POST을 통해 스토어에 변화가 일어남
})
```

* Store(스토어)
  * 스토어는 애플리케이션의 상태를 저장한다. 스토어는 정부관료와 같다고도 표현하며 모든 상태 변경은 스토어에 의해 결정되며 상태 변경을 위한 요청을 스토어에 직접 할 수는 없다. 상태 변경을 위해서는 꼭 액션 생성자를 통해 디스패쳐 단계를 거친 후 액션을 보내야만 상태값 변경이 가능하다.
* View or View Contoller
  * 뷰는 상태를 가져와 보여주고 사용자로 부터 입력 받을 화면을 보여준다. 컨트롤러 뷰는 스토어와 뷰의 중간 관리자 같은 역할을 하며 스토어에서 상태 값 변경이 일어났을 때 스토어는 그 사실을 컨트롤러 뷰에서 전달하며 컨트롤러 뷰는 자신 아래의 모든 뷰에게 새로운 상태를 넘겨준다.

여기 까지가 플럭스구조의 설명이며 플럭스 구조는 간단히 핵심만 생각하면 단방향 데이터 흐름을 생각해주면 될 것 같고 예시로는 리덕스 툴킷을 생각해도 될 것 같다.

* * *

### useReducer, useCallback

[참고 자료](https://goddaehee.tistory.com/311)

useReducer 훅이란 useState를 대신할 수 있는 함수이며 보통 리액트에서 컴포넌트의 상태 관리를 위해 가장 많이 사용되는 훅은 state이지만 좀 더 복잡한 상태 관리가 필요한 경우엔 reducer를 사용할 수 있다.

```js

let count = 0;
export default function Counter(){
function reducer(state){
  return {...state, x: state.x + 1}
}

const [, forceUpdate] = useReducer(reducer,{});
// const [ignored, forceUpdate] = useReducer(reducer,초기값);
// ignored의 경우 사용하지 않을 땐 지워둘 수 있다 대신 , 콤마는 있어야함

const handleClick = () => {
  count += 1;
  forceUpdate()
}
// 기존의 count는 let 변수로 생겨진 0을 업데이트를 해주면
// 재렌더링이 되지않아 화면에 숫자가 변하지않는데 useRedecer를 사용하여
// 강제로 렌더링을 시켜주는 모습?
return (
  // ....
)
}
```

숫자 하나를 늘려주는걸 함수로 빼준 모습이다.

```js
let count = 0;
export default function Counter(){
const [state,setState] = useState(0);

const forceUpdate = () => {
  setState(state + 1);
}

const handleCLick = () =>{
  count += 1;
  forceUpdate()
}
return (
  // ... 
)
}
```

기능을 다 구현해두었으면 매번 만드는 것 보다 하나의 훅으로 만들어주는게 편하다.

```js
// hooks/useForceUpdate.ts

export default function useForceUpdate(){
  const [state,setState] = useState(0);

  const forceUpdate = () =>{
    setStaet(state + 1)
  };
  return forceUpdate;
}
```

훅으로 분리시켜준 뒤 Counter.jsx에서 가져와 사용해주면 된다.

```js
let count = 0;
export default function Counter(){
  const forceUpdate = useForceUpdate();

  const handelClick = () =>{
    count += 1;
    forceUpdate()
  }
  return (
    // ...
  )
}
```

비교적 깔끔해진 코드를 확인해볼 수 있다. 여기서 약간 수정해주면

```js
const [, setState] = useState({});
const forceUpdate = () => setState({});
```

```js
function useForceUpdate() {
 const [, setState] = useState({});
 return useCallback(() => setState({}), []);
}
```

위와 같이 만들어서 항상 객체를 생성해줄 수도 있다.

여기서 useCallback은 함수를 항상 같은걸로 만들어준다. 이 함수가 항상 같아야 나중에 useEffect로 이 함수가 업데이트 될 시 렌더링을 해줄 수 있다.

* * *

### 최종적인 모습?

### Business Logic

```js
// Business Logic
const state = {
  count: 0,
};

function increase(){
  state.count += Math.ceil(Math.random() * 10);
}
```

### UI

```js
// UI

export default function Counter(){
  const forceUpdate = useForceUpdate();

  const handelClick = () => {
    increase();
    forceUpdate();
  }

  return (
    <div>
      <p>{state.count}</p>
      <button type="button" onClick={handelClick}>Increase</button>
    </div>
  )
}
```

이런식으로 관심사를 분리시켜줄 수 있다.

서로의 관심사가 각각 다른 것 이에 대한 장점으로는 비즈니스 로직의 경우는 코드가 크게 변경될 일이 없고 UI의 경우에만 변경될 수 있는데 자주 변경되지 않는 오래 유지되는 비즈니스 로직에 대한 테스트 코드를 작성해 유지보수에 도움이 되는 테스트 코드를 작성할 수 있다.

* * *

### 마무리

관심사의 분리는 여태 사용하던 리액트와 익숙하기도하며 살짝 다른 개념인듯하기도하다. 그렇지만 리액트를 계속 사용할 입장이라면 자연스레 익혀질 개념일 듯 싶다.