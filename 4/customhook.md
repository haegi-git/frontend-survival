# customHook

## 학습 키워드

* useRef
* Hook의 규칙

* * *

### CustomHook

[참고 자료](https://ko-de-dev-green.tistory.com/71)

커스텀 훅이란 말 그대로 개발자가 스스로 커스텀 한 훅을 말한다.

익숙해지면 굉장히 편리하게 사용할 수 있으며 만드는것 또한 쉽고 사용하기에도 재사용이 가능할 수 있으며 유용하게 사용이 가능하다.

주로 유저의 input을 관리할 때 혹은 Fetch를 요청할 때 커스텀 훅을 자주 사용된다.

예시로 커스텀 훅을 만들 폴더 및 파일을 만들어준 뒤 컴포넌트 만들듯 생성하면 된다.

```js
export default function useFetchProducts() {
  const [products, setProducts] = useState<Product[]>([]);
 
 useEffect(() => {
  const fetchProducts = async () => {
   const url = 'http://localhost:3000/products';
   const response = await fetch(url);
   const data = await response.json();
   setProducts(data.products);
  };

  fetchProducts();
 }, []);

 return products;
}
```

컴포넌트를 나누듯 똑같이 사용을하되 작명을 camelCase로 지어준다.

사용할 컴포넌트에서

```js
const products = useFetchProducts();
```

위 처럼 사용을 해주면 products에는 Fetch로 받아온 데이터가 들어가게된다.

커스텀 훅을 사용하게된다면 컴포넌트에서 데이터를 가져오기위해 작성한 코드들을 다 분리시켜줄 수 있기에 코드가 굉장히 깔끔해질 수 있다.

* * *

### Hook 규칙

[공식 문서](https://ko.legacy.reactjs.org/docs/hooks-rules.html)

1. 최상위에서만 훅을 호출해야 한다. - 반복문이나 조건문 혹은 중첩된 함수 내에서 호출하면 안된다.
2. 리액트 함수에서만 호출해야한다. - 일반 js에서 호출하면 안된다. react 함수 컴포넌트에서 또는 커스텀 훅에서 훅을 호출할 수 있다.

* 처음엔 콜백 함수 또는 조건문에서 훅을 호출하는 실수를 저지를 수 있다. (에러로 잘 알려주니 그때 고쳐나가면 될 듯 하다.)