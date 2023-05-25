# Routes

## 학습 키워드

* 라우터란?
* React Router
  * Browser Router
  * Route
  * Memory Router

* * *

### React Router

[참고 자료](https://poew.tistory.com/748)

[공식 문서](https://reactrouter.com/en/main)

리액트 라우터를 알기 전 라우팅에 대해 잠깐 알고가자면 다른 url 경로에 따라 다른 화면을 보여주는 걸 말한다. localhost/main 이라면 main 페이지를 localhost/about 이라면 about 페이지를

리액트 라우터는 SPA의 구조상 단일 페이지이므로 보여지는 모습이 바뀌어도 주소는 달라지지 않는다는 단점을 막아주기 위해 등장했고 아주 간단하게 페이지를 나누어줄 수도 있다.

사용하기 전 설치를 해주어야한다.

``
npm i react-router-dom
``

Routes로 Route를 감싸주어 사용하면 된다.

```ts
<Routes>
    <Route path="경로" element={라우트 할 컴포넌트} />
    <Route path="/" element={<HomePage />} />
    <Route path="/about" element={<AboutPage />} />
</Routes>
```

위 모습이 기본적인 리액트 라우터의 사용 예시이고 라우터를 사용하려면 브라우저 라우터를 잡아줘야한다.

```ts
// main.jsx 또는 App을 렌더하고 있는 곳

import { BrowserRouter } from 'react-router-dom';

root.render((
    <BrowserRouter>
        <App />
    </BrowserRouter>
))
```

브라우저 라우터로 앱을 감싸주기만하면 끝이다.

이제 주소창에 /about을 들어가면 about 컴포넌트를 띄워줄 수 있는 걸 볼 수 있다.

* * *

### 메모리 라우터

메모리 라우터는 리액트 라우터를 테스트 하기위해 사용된다.

```ts
// App.test.tsx
import { render } from '@testing-librart/react';
import { MemoryRouter } from 'react-router-dom';

import App from './App';

const context = describe

describe('App', () => {
 function renderApp(path: string) {
  render((
   <MemoryRouter initialEntries={[path]}>
    <App />
   </MemoryRouter>
  ));
 }
 
 context('when the current path is “/”', () => {
  it('renders the home page', () => {
   renderApp('/');

   screen.getByText(/Hello/);
  });
 });
 
 context('when the current path is “/about”', () => {
  it('renders the about page', () => {
   renderApp('/about');

   screen.getByText(/About/);
  });
 });
});
```

각각 페이지를 테스트 하는 코드이며 이곳에서 MemoryRouter가 사용이된다. 또한 MemoryRouter에는 initialEntries라는 속성이 붙는데 이곳에 경로를 넣어주는 듯 하다. 테스트 환경에서 사용된다는 걸 알아두면 될 것 같다.