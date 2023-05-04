# usehooks-ts

## 학습 키워드

* usehooks-ts
  * useBoolean
  * useEffectOnce
  * useFetch
  * useInterval
  * useEventListener
  * useLocalStorage
  * useDarkMode
* swr
* react-query

* * *

### usehooks-ts?

[공식 문서](https://usehooks-ts.com/)

usehooks-ts는 여러 커스텀 훅을 모아놓은 것 같다.

여기서 만들어진 걸 사용해도되지만 굳이 사용하지 않아도된다. 다만 공식 문서에 어떻게 만들어져있는지 코드가 그대로 나와있기에 많이 봐둔다면 커스텀 훅을 만들 때 도움이 많이 될 수 있다.

* useBoolean

토글을 만들 때 유용하다. not연산자를 사용하여 만들었던 걸 useBoolean으로 만들어주면 좀 더 명확하게 만들어줄 수 있다.

* useEffectOnce

말 그대로 useEffect를 한번만 사용하는 용도로 만들어졌다.

useEffect가 한번만 실행되는지 확인하기 위해서는 콘솔창을 이용하면 쉽게 알 수 있다.

* useFetch

데이터를 Fetch해올 때 사용한다.

```js
export default function useFetchproducts(){
cons url = '데이터를 가져올 경로';
const {data} = useFetch(url);
if(!data){
  return []
}
return data.products
}

```

위와 같은 모양으로 사용한다. 다른곳에서 products를 꺼내 사용하면 data를 받아와 사용할 수 있음

* useInterval

[정리 잘된 곳](https://velog.io/@goldbear2022/setInterval-%ED%8A%B9%EC%A7%95%EA%B3%BC-useInterval)

setInterval은 일정 시간 후 원하는 함수 호출 메서드이다.

setInterval은 주기적으로 실행해 일정 간격을 만들며 clearInterval을 이용해 함수호출을 중단해야함

react에서 setInterval을 사용하면 문제가 종종 생김,

```js
function Counter() {
  let [count, setCount] = useState(0);

  useInterval(() => {
    // Your custom logic here
    setCount(count + 1);
  }, 1000);

  return <h1>{count}</h1>;
}
```

* useEventListener

모든 종류의 이벤트를 확인할 수 있음 dispatchEvent로 전달되는 커스텀 이벤트에 반응하기 좋음

* useLocalStorage

localStorage와 JSON으로 객체 영속화

이벤트를 통해 다른 컴포넌트와 동기화하는 게 매우 중요한 특징
