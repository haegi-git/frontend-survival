# Global Style & Theme (아직 작성중)

## 학습 키워드

* Reset CSS
* box-sizing 속성
* word-break 속성
* Theme
* ThemeProvider

* * *

### Reset CSS

HTML에는 CSS가 기본적으로 들어가있는게 몇몇 존재한다.

리스트 스타일, 마진,패딩, 보더, 등등 . . . 여러가지가 존재하는데 이는 스타일을 잡는데 방해를 할 수 있기에 CSS를 초기화해주는 작업이 필요하다.

React를 사용하지 않았을 땐 CSS 파일로 Reset CSS라는게 존재했는데 react에서도 styled-reset 이라는게 존재한다.

[스타일 리셋](https://github.com/zacanger/styled-reset)

```bash
npm i styled-reset
```

패키지 설치를 해주고 App 컴포넌트에서 불러와주기만하면 끝이다.
(App이 아니더라도 모든걸 감싸는 컴포넌트에서 불러오면 된다.)

```js
export default function App() {
 return (
  <div>
   <Reset/>
   <Switch />
  </div>
 );
}

```

* * *

### Global Style

CSS 작업을 할 때 몇몇 속성들은 기본적으로 잡아두면 좋은게 있다.

box-sizing, font-size, word-break . . 등등

글로벌 스타일 또한 모든 컴포넌트를 사용할 App 또는 다른 최상위 컴포넌트에서 불러와 사용하면된다.

``src/styles`` 폴더에 GlobalStyle.ts을 생성 후 만들어 주자.

```js
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
 html {
  box-sizing: border-box;
 }
 
 *,
 *::before,
 *::after {
  box-sizing: inherit;
 }
 
 html {
  font-size: 62.5%;
 }
 
 body {
  font-size: 1.6rem;
 }
 
 :lang(ko) {
  h1, h2, h3 {
   word-break: keep-all;
  }
 }
`;

export default GlobalStyle
```

글로벌 스타일로 잡은 스타일을 몇가지 알아보면

* html에 기본적으로 font-size: 62.5%를 줌으로써 추후 폰트사이즈들을 rem으로 설정할 수 있게끔 만들어준다. (62.5%로 잡음으로써 1rem = 10px)

* :lang(ko)는 한국어에 대한 설정으로 h1,h2,h3태그에 word-break 속성을 넣어주는 것이므로 word-break에 대한건 [참고](https://developer.mozilla.org/ko/docs/Web/CSS/word-break) 이곳에서 미리 확인해볼 수 있다. (이상하게 문장이 이어가다 중간에 끊기는 일이 생기지 않도록 해주는 옵션)

* html에 box-sizing은 요소의 너비와 높이에 대한 속성으로 마진 패딩으로 인해 글자 또는 컨텐츠의 너비가 이상해보일 수 있는데 그럴 때 사용해주는 옵션으로 알고있다. [참고](https://developer.mozilla.org/ko/docs/Web/CSS/box-sizing) 이곳에서 미리 확인해볼 수 있다.

위 처럼 잡아준 뒤 GlobalStyle을 reset과 동일하게 불러와주면 끝이다.

* * *

### Theme

[Theming](https://styled-components.com/docs/advanced#theming)

앞서 배운 모든건 Theme를 사용할 때 큰 도움이 된다.

Theme은 기본적으로 제공해주며 어떨 때 사용을하느냐? 다크모드같은걸 활용할 때 자주 사용되는데

기본적인 전체 디자인의 속성?을 미리 잡아두고 꺼내와 사용한다는 느낌인 것 같다.

디자인 시스템에 대응하기위해 꺼내오기 위한 이름을 알아보기 쉽게 정해놓는 듯 하다.

error에 관한 색상이나 옵션이라면 error, dark모드에 관한거라면 dark,

```js
const defaultTheme = {
    colors: {
        background : '#fff',
        text : '#000',
        primary : '#f00',
    }
}
```

등등 예시처럼 미리 지정을 변수에 옵션을 지정해두는 걸 빼오는 느낌이며 기본적인 css를 담아두고, dark모드의 css를 담아두고 그걸 빼와서 사용하여 추후 유지보수에 도움이 많이 될 것 같다.

기본 색상으로 검정을 사용했다가 추후 파랑으로 변경사항이 생긴다면 이곳만 관리하여 모든걸 관리해줄 수 있는 이점이 생기는 것 같다.

* 사용 예시

``src/styles`` - defaultTheme.ts, darkTheme.ts 생성 후

```js
const defaultTheme = {
 colors: {
  background: '#FFF',
  text: '#000',
  primary: '#F00',
  secondary: '#00F',
 },
};

export default defaultTheme;
```

```js
const darkTheme = {
 colors: {
  background: '#FFF',
  text: '#000',
  primary: '#F00',
  secondary: '#00F',
 },
};

export default darkTheme;
```

기본Theme과 darkThem을 생성한 뒤 타입또한 잡아주어야한다.

``src/styles`` Theme.ts 파일 생성 후

```js
import defaultTheme from './defaultTheme';

type Theme = typeof defaultTheme;

export default Theme;
```

```js
const darkTheme: Theme = {
 colors: {
  background: '#FFF',
  text: '#000',
  primary: '#F00',
  secondary: '#00F',
 },
};

export default darkTheme;
```

다크모드에 타입을 잡아주면 된다.

그리고 Theme을 사용하기위해 redux처럼 provider로 감싸주어야한다. 최상위 태그에 ThemeProvider로 모든걸 감싸주면된다.

```js

export default function App() {
 const theme = defaultTheme;
 return (
  <ThemeProvider theme={theme}>

   <GlobalStyle />
   <Reset/>
   <Switch />

  </ThemeProvider>
 );
}

```

Theme을 설정했으니 전역스타일에서 사용해주면 된다. 기존에 만들어둔 글로벌스타일에서

```js

const GlobalStyle = createGlobalStyle`
    html {
  box-sizing: border-box;
 }
 
 *,
 *::before,
 *::after {
  box-sizing: inherit;
 }
 
 html {
  font-size: 62.5%;
 }
 
 body {
  font-size: 1.6rem;
  background-color: ${props => props.theme.color.background};
 }
 
 :lang(ko) {
  h1, h2, h3 {
   word-break: keep-all;
  }
 }
`;
```

props로 theme을 받아와 사용하면되는데 타입에러가 나타난다. 그 타입 에러를 막기위해 ``src/styles`` styled.d.ts 파일을 생성해줘야한다.

```js
import 'styled-components';

declare module 'styled-components' {
 export interface DefaultTheme extends Theme {
  colors: {
   background: string;
   text: string;
   primary: string;
   secondary: string;
  }
 }
}
```

위와 같이 타입을 정의하고 하나씩 잡아주는 것은 불편하기에 반대로 defaultTheme에서 타입을 추출하면 된다.

```js
import 'styled-components';

import Theme from './Theme';

declare module 'styled-components' {
 export interface DefaultTheme extends Theme {}
}
```

이렇게 사용을 해주면 좀 더 편하게 사용할 수 있다.

이제 이렇게 세팅해놓은걸 바탕으로 다크모드를 구현할 수 있다. 다크모드를 구현할 땐 커스텀훅 중 useDarkMode를 사용해주면 된다.

useDarkMode에는 toggle또한 지원을 해준다.

```js
export default function App(){
    const { isDarkMode, toggle } = useDarkMode();

    const theme = isDarkMode ? darkTheme : defaultTheme;
}