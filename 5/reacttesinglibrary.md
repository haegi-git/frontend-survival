# React Testing Library

## 학습 키워드

* React Testing Library
* given - when - then 패턴
* Mocking
* Test fixture

* * *

### React Testing Library?

[참고 자료](https://doiler.tistory.com/57)

[공식 자료](https://testing-library.com/docs/react-testing-library/intro/)

React Testing Library는 Jest와 다른 테스트 라이브러리이며 React Testing Library는 사용자가 컴포넌트를 사용하는 것 처럼 테스트를 작성할 수 있게 설계되어있다.

둘의 차이로 React Testing Library는 컴포넌트를 테스트하는 , 리액트 컴포넌트의 기능, 화면에 표시되는 내용을 테스트를 위함이고

Jest는 자바스크립트 코드의 기능을 테스트 하기 위한 프레임워크 라고 나온다.(GPT)

React Testing Library는 사용방법, 예시들을 위주로 기록하여 이해를 하는게 가장 좋을 듯 하다.

예시

```js
import { render, screen } from '@testing-library/react';

import TextField from './TextField';

test('TextField', () => { 
    // given
 const text = 'Tester';
 const setText = () => {
  // do nothing...
 };
    // when
 render(( 
  <TextField
   label="Name"
   placeholder="Input your name"
   text={text}
   setText={setText}  
  />
 ));
 // then
 screen.getByLabelText('Name');
});
```

label이 name이 같은지 확인하는 테스트 코드인데 모든 코드들을 빡빡하게 다 테스트 시켜줄 수도 있다.

```js
import { render, screen, fireEvent } from '@testing-library/react';

import TextField from './TextField';

const context = describe;

describe('TextField', () => {
 const text = 'Tester';
 const setText = jest.fn();
 
 beforeEach(() => {
  setText.mockClear();
  // 또는 jest.clearAllMocks(); 
 });
 
 function renderTextField() {
  render((
   <TextField
    label="Name"
    placeholder="Input your name"
    text={text}
    setText={setText}
   />
  ));
 }
 
 it('renders an input control', () => {
  renderTextField();

  screen.getByLabelText('Name');
 });
 
 context('when user types text', () => { 
  it('calls the change handler', () => {
   renderTextField();

   fireEvent.change(screen.getByLabelText('Name'), {
    target: {
     value: 'New Name',
    },
   });
 
   expect(setText).toBeCalledWith('New Name');
  });
 });
});
```

교재의 예제 내용인데 아직까지 완벽히 이해는 되지않는다. context, it, expect, 등 간단한건 이해가가지만 새로운 메서드들이 있기에 좀 더 검색해보고 알아봐야할 것 같다.

mock을 이용해 외부의존성이 큰 코드를 작성할 때 해당부분을 가짜로 작성도 가능하다.

```js
import { render, screen } from '@testing-library/react';

import App from './App';

jest.mock('./hooks/useFetchProducts', () => () => [
 {
  category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
 },
]);

test('App', () => {
 render(<App />);

 screen.getByText('Apple');
});
```

외부에서 fetch해오는 코드를 mock으로 처리한 모습인데 아직 완벽히 이해가되지않기에 좀 더 공부를 해봐야할 것 같다.

* * *

### Test Fixture란

중복으로 발생하는 무언가를 고정시켜 한곳에서 관리하는 것

프론트엔드의 경우 백엔드와 통신하는 경우가 많은데 그 부분을 fixture에서 관리를 해주는 것

* * *

### 마무리

React Testing Library도 그렇고 Mock도 그렇고 처음 겪어보는 것과 처음보는 메서드들이 많기에 전체 코드를 이해하기 위해서는 각 메서드가 무엇을 의미하는지를 알아야할 것 같다.

사용방법에 대해서는 BDD스타일의 코드로 작성한 예시를 위주로 공부를 해주면 좋지않을까 생각한다.

이 부분의 강의는 몇 차례 더 봐야 이해가될 듯 하고 좀 더 많이 알아봐야할 것 같다. 아직까지 내용이 부실할 수 있지만 좀 더 공부를 해가며 채워넣어야겠다.