# CSS-in-JS

## 학습 키워드

* CSS in JS 란
* CSS

* * *

### CSS in JS ?

[참고 자료](https://velog.io/@willy4202/styled-components%EC%9D%98-%EC%82%AC%EC%9A%A9%EC%9D%B4%EC%9C%A0%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90.-css-in-js)

css-in-js는 자바스크립트 코드로 CSS를 작성하는 방식이며 다음과 같은 문제를 해결하기 위해 나온 기술이다.

* Global namespace - 글로벌 공간에 선언된 이름의 명명 규칙 필요
* Dependencies - CSS간의 의존 관계를 정리
* Dead Code Elimination - 미사용 코드 검출
* Minification - 클래스 이름의 최소화
* Sharing Constants - JS와 CSS의 상태 공유
* Non-deteministic Resolution - CSS 로드 우선 순위 이슈
* Isolation - CSS와 JS의 상속에 따른 격리 필요 이슈

css-in-js를 사용하기위해 여러 라이브러리가 존재하며 대표적으로 styled-components를 많이 사용한다.

* 장단점

css-in-js를 사용하면 CSS파일의 유지보수가 필요 없어진다. 컴포넌트 레벨로 추상화하기 때문에 단일 파일에서 관리가 가능하다. 또한 js코드를 활용할 수 있다.

해당 DOM에서만 활용할 수 있는 것도 장점으로 꼽을 수 있으며 자바스크립트와 CSS 사이에 있는 상수와 함수를 공유할 수 있다. 거기다 스타일링을 위한 코드 사용량이 줄어든다.

그러나 러닝커브가 높다는 단점이 있다. 또한 별도의 라이브러리가 필요해 크기가 커질 수 있고 디자인 페이지를 작업한다면 CSS 모듈 방식에 비해 느린 성능을 보여줄 수 있다.

* 스타일 컴포넌트가 핵심

[위키피디아](https://en.wikipedia.org/wiki/CSS-in-JS)

```js
import styled from 'styled-components';
// Create a component that renders a <p> element with blue text
const BlueText = styled.p`
  color: blue;
`;

<BlueText>My blue text</BlueText>
```

BlueText 라는 컴포넌트를 만들어 사용하는 예제의 모습이다.

* * *

### CSS

[참고 자료](https://developer.mozilla.org/ko/docs/Learn/Getting_started_with_the_web/CSS_basics)

CSS는 프로그래밍 언어가 아니며 마크업 언어도 아니다. 스타일 시트 언어이며 HTML 문서에 있는 요소들에 선택적으로 스타일을 적용할 수 있다는 말이다.

CSS에서도 알아두면 좋을게 많지만 이곳에 모든걸 다 작성해둘 순 없으니 추후 알아보면 좋을 것만 작성

Flexbox,Gird,media query, 선택자, 박스모델 등등
