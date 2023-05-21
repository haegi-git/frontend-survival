# Redux

## 학습 키워드

* Redux
* Reflect

* * *

### Redux?

[참고 자료](https://velog.io/@youthfulhps/What-is-Redux-and-why-use-it)

리덕스는 일단 상태 관리 라이브러리로 리액트는 단방향 데이터 흐름을 갖고 있기에 그에 따른 불필요한 리렌더링, props drilling 등의 문제가 있기 때문에 상태 관리 라이브러리를 사용한다.

나는 일단 리덕스 툴킷을 조금 배워서 사용을 했었고 그에 따른 경험으로는 store에서 모든걸 관리하며 store에서 만들어 둔 기능을 가져다 사용한다 라고 배웠다.

그렇게 되면 장점으로 모든 기능들은 store에서 관리해주면 된다. 그리고 또한 버그가 생겼을 때도 store만 살펴보면 해결해줄 수 있기에 유용하게 사용될 수 있다.

강의에서 나온 예제

src/stores/BaseStore.ts 파일

```ts
export type Action<Payload> = {
 type: string;
 payload?: Payload;
}

type Reducer<State, Payload> = (state: State, action: Action<Payload>) => State;

type Reducers<State> = Record<string, Reducer<State, any>>;

type Listener = () => void;

export default class BaseStore<State> {
 state: State;

 reducer: Reducer<State, any>;

 listeners = new Set<Listener>();
 
 constructor(initialState: State, reducers: Reducers<State>) {
  this.state = initialState;

  this.reducer = (state: State, action: Action<any>): State => {
   const reducer = Reflect.get(reducers, action.type);   
   if (!reducer) {
    return state;
   }
   return reducer(state, action);
  };
 }
 
 dispatch<T>(action: Action<T>) {
  this.state = this.reducer(this.state, action);
  this.listeners.forEach((listener) => listener());
 }
 
 addListener(listener: Listener) {
  this.listeners.add(listener);
 }
 
 removeListener(listener: Listener) {
  this.listeners.delete(listener);
 }
}
```

src/stores/Store.ts 파일이며 이곳에서 거의 모든 기능과 요소를 만들어 둔다.

```ts
import { singleton } from 'tsyringe';

import BaseStore, { Action } from './BaseStore';

const initialState = {
 count: 0,
 name: 'Tester',
};

export type State = typeof initialState;

function increase(state: State, action: Action<number>) {
 return {
  ...state,
  count: state.count + (action.payload ?? 1),
 };
}

function decrease(state: State) {
 return {
  ...state,
  count: state.count - 1,
 };
}

const reducers = {
 increase,
 decrease,
};

@singleton()
export default class Store extends BaseStore<State> {
 constructor() {
  super(initialState, reducers);
 }
}
```

```ts
import { container } from 'tsyringe';

import { Action } from '../stores/BaseStore';

import Store from '../stores/Store';

export default function useDispatch<Payload>() {
 const store = container.resolve(Store);
 return (action: Action<Payload>) => store.dispatch(action);
}
```

```ts
import { container } from 'tsyringe';

import { useEffect, useState } from 'react';

import Store, { State } from '../stores/Store';

import useForceUpdate from './useForceUpdate';

type Selector<T> = (state: State) => T;

export default function useSelector<T>(selector: Selector<T>): T {
 const store = container.resolve(Store);
 
 const [state, setState] = useState<T>(selector(store.state));
 
 const forceUpdate = useForceUpdate();
 
 useEffect(() => {
  const update = () => {
   const newState = selector(store.state);
   // TODO: T가 object일 때 처리 필요함.
   if (newState !== state) {
    setState(newState);
    forceUpdate();
   }
  };
 
  store.addListener(update);
  return () => store.removeListener(update);
 }, [store, forceUpdate]);

 return state;
}
```

아래는 dispatch와 selector을 사용해 기능과 원하는 요소를 가져다 사용한 모습이다.

```ts
const dispatch = useDispatch();
const count = useSelector((state) => state.count);

dispatch({ type: 'increase' });
dispatch({ type: 'decrease' });

dispatch({ type: 'increase', payload: 10 });
```

아직까지 코드를 100퍼센트 이해할 순 없지만 리덕스 툴킷을 사용했을 때를 생각해보면 어느정도 충분히 이해는 된다.

하지만 어려운점은 타입스크립트가 섞여있다보니 아직 익숙치않아 어렵다.

또한 파일이 많이 분리되는 점에서 내가 작업했었던 방식과 너무나 달라 이해하는데 꽤나 오랜시간이 들었었고 그렇기에 좀 더 열심히 공부해야할 것 같다.

추후에 리덕스 툴킷을 더 공부할 수도 있을 듯 하다. (리덕스 툴킷이 좀 더 사용하기 쉽게 배웠었기 때문에..)
