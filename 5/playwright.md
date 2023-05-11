# Playwright

## 학습 키워드

* E2E(End to End) Test
* Headless Chrome
* Puppeteer
* Playwright
* CodeceptJS

* * *

### E2E Test

E2E 테스트는 End to End 테스트의 약자로 애플리케이션의 흐름을 처음부터 끝까지 테스트 하는 것을 의미한다.

* E2E test를 수행하는 이유

1. 사용자 중심의 테스트 - e2e 테스트는 사용자 관점에서 애플리케이션을 테스트하기에 사용자가 경험하는 모든 상황을 시뮬레이션하여 애플리케이션의 실제 동작을 평가할 수 있다.
2. 버그 식별 - e2e 테스트를 통해 전체 애플리케이션 흐름을 검증 할 수 있기 때문에 다양한 시나리오에서 발생하는 잠재적인 버그와 결함을 찾을 수 있음
3. 효율적인 테스트 - e2e테스트를 자동화 할 수 있으므로 반복적인 작업과 인간의 오류를 최소화하여 효율적으로 테스트를 수행할 수 있음

* E2E test 장점

1. 애플리케이션의 완전한 기능성을 확인할 수 있음
2. 사용자 중심의 테스트를 수행할 수 있으므로 사용자 경험 개선 가능
3. 효율적으로 테스트를 수행할 수 있으며 자동화가 가능하다.

* 단점

1. 테스트를 작성하고 유지보수하는 데 시간과 노력이 필요함
2. e2e 테스트가 너무 복잡하거나 잘못 작성되면 실행 속도가 느려질 수 있음
3. 모든 시나리오를 커버하기에 테스트가 부족할 수 있음

* * *

### Headless Chrome

Headless Chrome은 Chrome 브라우저의 Headless모드이다.

Headless Chrome은 웹 애플리케이션을 테스트하거나 스크린샷 생성 , 웹 스크래핑에 사용된다. 크롬 개발자 도구의 기능과 호환되며 자바스크립트 코드를 사용하여 브라우저를 제어가능하다. 이를 통해 웹페이지를 탐색하고 HTML을 분석하고 요소를 선택하며 사용자와 상호 작용하며 자동화된 테스트를 수행 가능하다.

Headless Chrome은 테스트와 웹스크래핑 등 작업을 자동화하기 위한 유용한 도구이다.

* * *

### Puppeteer

Puppeteer은 노드js환경에서 Headless Chrome를 제어하는 API를 제공하는 라이브러리이다. Puppeteer는 웹 애플리케이션 테스트, 스크래핑, 크롤링 등 다양한 작업을 자동화하기 위해 사용된다.

Puppeteer를 사용하는 이유로는 웹 애플리케이션 테스트와 스크래핑, 웹 페이지 자동화, PDF및 스크린샷 생성, 브라우저 테스트 등이있다.

* * *

### Playwright?

Playwright은 Pupperteer처럼 브라우저 자동화 도구이며 Nodejs환경에서 실행된다. 자바스크립트나 타입스크립트 모두 사용 가능하며 브라우저를 제어할 수 있다.

* Puppteer와 Playwright의 차이?

1. 지원하는 브라우저에서 차이가 있다.
    * Pupperteer은 Chrome 및 Chromium 브라우저에 의존하며
    * Playwright은 Chromium,Firefox 및 WebKit 기반 브라우저에 실행 가능하다 이로 인해 멀티 브라우저 자동화가 가능하다.
2. 멀티 페이지 탭
    * Pupperteer은 하나의 페이지만 제어 가능하다
    * Playwright은 여러개의 페이지나 탭을 동시에 제어가능하며 이를 통해 멀티페이지 탭을 처리할 수 있다.
3. 자동화 속도
    * Playwright가 Pupperteer보다 자동화 속도가 빠르다는 장점이 있다. 이는 Playwright가 자동화 중 직접적으로 Chrome DevTools Protocol을 사용해 제어하기 때문이다.
4. 다양한 기능
    * Playwright가 Pupperteer보다 다양한 기능을 제공해준다. 예를 들어 페이지 내의 동적 대기 시간을 처리하기 위한 지연 기능을 제공하며 멀티 브라우저 제어 , 다중 쓰레딩, 비동기 네트워크 요청 처리 등의 기능을 지원해준다.

강의에서는 Playwright를 사용을 했다.

사용하기 위해서는 설치를 해주어야하고 간단한 설정을 해줘야한다.

* 설치 및 설정

* ``npm i -D @playwright/test eslint-plugin-playwright`` 설치
* playwright.config.ts 파일 생성

```js
// playwright.config.ts
import { PlaywrightTestConfig } from '@playwright/test';

const config: PlaywrightTestConfig = {
 testDir: './tests',
 retries: 0,
 use: {
  baseURL: 'http://localhost:8080', // 리액트 앱의 포트
  headless: !!process.env.CI,
  screenshot: 'only-on-failure',
 },
};

export default config;
```

* tests/.eslintrc.js 파일 생성

```js
module.exports = {
 env: {
  jest: false,
 },
 extends: ['plugin:playwright/playwright-test'],
 rules: {
  'import/no-extraneous-dependencies': 'off',
 },
};
```

* tests/home.spec.ts 파일 생성
  * 이곳에서 테스트를 진행하면 된다.
  * 참고로 여기서의 test와 expect는 jest와 다르며 그렇기에 eslint에서 jest를 꺼둔것이다.

```js
