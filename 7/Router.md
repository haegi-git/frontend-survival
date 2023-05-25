# Router

## 학습 키워드

* ReactRouter - RouterProvider

* * *

이번 라우터의 주요 핵심은 라우터 객체를 만들어 사용하는 방법(6.4 버전 부터 지원)

### 객체로 만드는 방법

```ts
// routes.tsx
import { Outlet } from 'react-router-dom';

function Layout() {
 return (
  <div>
   <Header />
   <Outlet />
   <Footer />
  </div>
 );
}

const routes = [
 {
  element: <Layout />,
  children: [
   { path: '/', element: <HomePage /> },
   { path: '/about', element: <AboutPage /> },
  ],
 },
];

export default routes;
```

객체로 만들어 파일을 분리해주어 사용해줄 수 있다. 화면에 렌더되는 부분을 Layout으로 잡아주어 사용해줄 수도 있다.

위 처럼 사용을 해주면 App을 거치지않고 바로 사용해줄 수도 있다.

아직까진 생소한 모습이라 적응하려면 좀 더 사용을 해봐야겠다.

또한 위와 같이 사용을하면

```ts
// App.tsx
import {RouterProvider, createBrowserRouter} from 'react-router-dom';

import routes from './routes';

const router = createBrowserRouter(routes);

export default function App() {
 return (
  <RouterProvider router={router}/>
 );
}

```

앱이 이러한 모습으로 전에 사용한 테스트코드는 무용지물이되므로 새로 작성해줘야한다.

```ts
import {render, screen} from '@testing-library/react';

import App from './App';
import {MemoryRouter, RouterProvider, createMemoryRouter} from 'react-router-dom';
import routes from './routes';

const context = describe;

describe('routes', () => {
 function renderRouter(path: string) {
  const router = createMemoryRouter(routes, {initialEntries: [path]});
  render(<RouterProvider router={router}/>);
 }

 context('여기는 메인페이지', () => {
  it('렌더 메인페이지', () => {
   renderRouter('/');
   screen.getByText(/메인페이지/);
  });
 });

 context('여기는 어바웃페이지', () => {
  it('렌더 어바웃페이지', () => {
   renderRouter('/about');
   screen.getByText(/About페이지/);
  });
 });
});

```

새롭게 작성된 테스트 코드이며 여기서는 App을 테스트하는 것이 아니라 routes.tsx를 테스트해주면 라우터에 관한 테스트를 해줄 수 있다.

아직까지 객체로 만들어 사용하는 것에 대한 장점이 잘 느껴지지않아 잘 모르겠고 생소한 모습이라 좀 더 사용해보며 익숙해져봐야할 것 같다.

* * *

### GPT에게 물어본 장점

1. 컴포넌트 간 라우팅 관리 - 라우터 객체를 사용하면 애플리케이션의 여러 컴포넌트 간에 라우팅을 효율적으로 관리가 가능하다.
2. 중첩된 라우팅 관리 - 라우터 객체는 중첩된 라우팅을 처리하는데 도움이 된다. 중첩된 라우트 구조에서 여러 단계의 컴포넌트 계층을 표현할 수 있으며 라우터 객체를 사용하면 이러한 계층 구조를 쉽게 관리 할 수 있다.
3. 라우팅 기능 확장 - 라우터 객체를 사용하면 리액트 라우터 라이브러리의 기능을 확정할 수 있다. 기본적인 라우팅 이외에도 사용자 정의된 라우팅 규칙을 적용하거나 특정 이벤트에 대한 처리하는 로직을 추가하는 등의 작업을 할 수 있다.
4. 테스트 용이성 - 라우터 객체를 사용하면 테스트 용이성이 향상된다. 일반 컴포넌트 형태로 라우팅을 다룰 땐 라우팅 로직을 테스트하기 어려울 수 있으나 라우터 객체를 사용하면 라우팅 로직을 분리하고 테스트하기 쉽게 만들 수 있다.