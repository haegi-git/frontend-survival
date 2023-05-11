# MSW

## 학습 키워드

* Service worker
* MSW(Mock Service Worker)
* polyfill(폴리필)

* * *

### Service worker

[참고 자료](https://2ham-s.tistory.com/409)

서비스 워커는 브라우저가 백그라운드에서 실행하는 스크립트이며 웹페이지와 별개로 생명주기를 갖고 동작한다.

장점으로

1. 브라우저의 파일을 캐시할 수 있고
2. Request를 가로채 Proxy Server와 비슷하게 동작한다.

사용 목적으로는(GPT)

1. 오프라인 기능 - 웹 애플리케이션이 오프라인 상태에서 작동할 수 있도록 도와준다. 이를 위해 서비스 워커는 네트워크 요청을 가로채고 캐싱된 리소스를 사용하여 응답을 제공하도록 프로그래밍 해야한다.
2. 빠른 로딩 속도 - 서비스 워커는 캐싱된 리소스를 사용해 웹 페이지를 더 빠르게 로딩할 수 있도록 도와준다.
3. 백그라운드 동기화 - 서비스 워커는 백그라운드에서 실행되므로 사용자가 애플리케이션을 사용하지 않을 때에도 데이터를 동기화할 수 있다. 예시로 오프라인에서 메모를 작성 후 인터넷 연결이 복구되면 서비스 워커가 백그라운드에서 메모를 서버에 동기화할 수 있다.
4. 푸시 알람 - 서비스 워커는 백그라운드에서 실행될 수 있으므로 푸시 알람을 구현하는데 사용된다.
5. 안전한 환경 - 서비스 워커는 브라우저의 보안 모델을 사용하여 악성 스크립트로부터 사용자를 보호한다. 이는 서비스 워커가 웹 페이지와 독립적으로 실행되며 웹 페이지에서 제어할 수 없도록 설계 되었기 때문이다.

* * *

### MSW(Mock Service Worker)

Mock Service Worker는 Express와 비슷하게 생겼지만 조금 더 불편한 오프라인에서 사용하는 도구이다.

또한 Service Worker와는 직접적인 관련이 없다.

코드 레벨이 아닌 네트워크 레벨에서 가짜를 구현, 오프라인 작업 등을 지원하기 위한 서비스 워커의 기능을 활용한 것

백엔드에서 API가 완성이 되지 않았을 때 프론트에서 유용하게 사용할 수 있는 도구이다. 백엔드 API와의 통신을 가상으로 시뮬레이션을 하여 프론트의 코드를 테스트 및 개발을 할 때 사용한다.

전 시간 React Testing Library에서도 mock 메서드를 사용했었는데 거기서 사용된 mock은 테스트를 작성할 때 모듈의 특정 함수 또는 클래스의 동작을 가상화하거나 특정 조건에서 테스트를 위해 새로운 반환값을 생성할 수 있도록 도와주는 메서드이고

MSW에서의 mock은 네트워크 레벨에서 HTTP 요청과 응답을 가로채 가상화하는 도구이다. MSW의 mock은 가상 서버를 생성하며 백엔드가 준비되기 전 프론트에서 API를 요청을 가로채 처리할 수 있다.

* MSW를 사용하는 대표적인 이유와 장점 (GPT)

1. 독립적인 테스트 환경 구축 - MSW는 클라이언트 측에서 가짜 API를 생성하는 데 사용이된다. 이를 통해 의존성 없이 클라이언트 측 코드를 테스트할 수 있다. 따라서 테스트 환경을 독립적으로 구축하여 효율적인 단위 및 통합 테스트를 진행할 수 있다.
2. 개발 속도 향상 - MSW를 사용하면 개발자가 빠르게 API 응답을 구현할 수 있다. 서버와의 의존성 없이 클라이언트 측에서 API응답을 구현할 수 있으므로 전체 시스템의 개발 속도가 향상된다.
3. 더 나은 에러 핸들링 - MSW를 사용하면 API 응답을 강제로 실패시키거나 지연시키는 등의 행동을 할 수 있다. 이를 통해 클라이언트 측에서 API 오류 및 네트워크 오류 등의 예외 상황을 더 효율적으로 처리할 수 있다.
4. API 테스트 및 모의 - MSW를 사용하면 클라이언트 측에서 API 응답을 모의(mock)할 수 있다. API가 실제로 호출되지 않아도 클라이언트 측에서 응답을 생성하여 테스트 할 수 있다. 서버가 아직 준비되지 않아도 클라이언트 측에서 응답을 모의하여 개발 가능하다.
5. 더 나은 디버깅 - 클라이언트 측에서 API 요청 및 응답을 모니터링 할 수 있다. 이를 통해 네트워크 오류나 API 호출 문제 등의 문제를 더 쉽게 디버깅 가능하다.

* 단점 (GPT)

1. 추가 코드 및 복잡성 - MSW를 사용하면 응답을 생성하는 코드를 작성해야한다. 이는 추가 코드 및 복잡성으로 이어질 수 있다. 또한 서버 의존성을 없애는 대신 클라이언트 측에서 가짜 API를 생성하므로 불필요한 코드 복잡성이 생길 수 있다.
2. 서버와 동기화 - MSW를 사용하면 클라이언트 측에서 가짜 API를 생성해야하기에 서버와의 API 응답이 일치하지 않을 수 있다. 따라서 서버와 동기화되어 응답이 일치하도록 유지해야한다.
3. 네트워크 오버헤드 - MSW는 서비스 워커를 사용하여 동작한다. 서비스 워커는 네트워크 계층에서 작동하므로 오버헤드가 발생할 수 있다. 그러므로 서비스 워커의 성능을 고려해 최적화를 수행해야한다.
4. 특정 상황에서 테스트 오류 - MSW를 사용할 때 특정 상황에서는 테스트 오류가 발생할 수 있다. 예시로 로그인과 같은 인증이 필요한 API 요청의 경우 테스트 오류가 발생할 수 있다.
5. 잘못된 테스트 - 클라이언트에서 가짜 API를 생성하므로 잘못된 테스트가 발생할 수 있다. 예를 들어 응답을 강제로 실패시키는 것이 적절하지않은 경우 잘못된 테스트 결과를 발생할 수 있다.

### 사용 예시

* 설치부터 해주어야한다.
* ``npm i -D msw``
* jest.config.js 파일의 "setupFilesAfterEnv” 속성에 setupTests.ts 파일 추가.

```json
module.exports = {
 testEnvironment: 'jsdom',
 setupFilesAfterEnv: [
  '@testing-library/jest-dom/extend-expect',
  '<rootDir>/src/setupTests.ts',
 ],
 transform: {
  '^.+\\.(t|j)sx?$': ['@swc/jest', {
   jsc: {
    parser: {
     syntax: 'typescript',
     jsx: true,
     decorators: true,
    },
    transform: {
     react: {
      runtime: 'automatic',
     },
    },
   },
  }],
 },
};
```

* 파일 생성 src/setupTests.ts

```js
// setupTests.ts
import server from './mocks/server';

beforeAll(() => server.listen({ onUnhandledRequest: 'error' }));

afterAll(() => server.close());

afterEach(() => server.resetHandlers());
```

* src/mocks/server.ts 파일 생성

```js
import { setupServer } from 'msw/node';

import handlers from './handlers';

const server = setupServer(...handlers);

export default server;
```

* src/mocks/handelrs.ts 파일 생성
  * Express와 유사하다.

```js
import { rest } from 'msw';

const BASE_URL = 'http://localhost:3000';

const handlers = [
 rest.get(`${BASE_URL}/products`, (req, res, ctx) => {
  const products = [
   {
    category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
   },
  ];

  return res(
   ctx.status(200),
   ctx.json({ products }),
   );
  }),
 ];

export default handlers;
```

* 만약 fixtures를 준비해뒀다면 fixtrues를 사용해도 된다.

```js
import { rest } from 'msw';

import fixtures from '../../fixtures';

const BASE_URL = 'http://localhost:3000';
// const BASE_URL = process.env.API_BASE_URL || 'http://localhost:3000';
// 이 모양을 가장 많이 사용한다.

const handlers = [
 rest.get(`${BASE_URL}/products`, (req, res, ctx) => {
  const { products } = fixtures;

  return res(
//    ctx.status(200),
   ctx.json({ products }),
   );
  }),
 ];

export default handlers;
```

* App.test.ts 파일 생성
  * waitFor 안에 있는게 될때까지 기다려주기

```js
import { render, screen, waitFor } from '@testing-library/react';

import App from './App';

// jest.mock 불필요.

test('App', async () => {
 render(<App />);
 
 await waitFor(() => {
  screen.getByText('Apple');
 });
});
```

지금 당장에야 이걸 본다고 이해가되진 않을거같다.

조금 더 사용을 해보거나 많이 겪어봐야 이해를 할 수 있을 듯 하다.

지금은 이런식으로 사용을하고 어떠한 도구인지만 알고 넘어가되 계속 사용을하며 이해를 하도록 해보자.

또한 너무 열심히 만들면 백엔드 개발하게되니 주의

* * *

### polyfill(폴리필)

[깃허브에서 만든 fetch polyfill](https://github.com/github/fetch)

폴리필은 브라우저가 지원하지 않는 자바스크립트 코드를 지원 가능하도록 변환한 코드를 말한다. 하위 브라우저가 지원하는 자바스크립트 코드를 사용해 최신 기능을 똑같이 구현하는 방식이다.

``npm i -D whatwg-fetch``

설치 해준 뒤 setupTests.ts에 import해주면 된다.

```js
import 'whatwg-fetch';

import server from './mocks/server';

beforeAll(() => server.listen({ onUnhandledRequest: 'error' }));

afterAll(() => server.close());

afterEach(() => server.resetHandlers());
```

사용하는 이유는 최신 node에는 fetch가 있지만 전 버전에서? 없을 수도 있어서 인것 같다.

* * *

### 마무리

MSW 강의만 네번 정도 돌려본 것 같은데 아직까지도 제대로 이해가 되지않는다....

처음 들어보는 단어도 많고 처음 들어보는 코드에 처음 접해보는 것들 투성이라 아직까지는 너무 어렵다.

계속해서 진행하다보면 조금 나아질 수 있을지 모르겠다..!
