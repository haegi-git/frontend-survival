## 테스팅 도구

### 학습 키워드
* Jest
* Describe-Context-It 패턴
* React Testing Library

***

## Jest

[Jest 공식문서](https://jestjs.io/)   

거의 모든 것을 갖춘 테스팅 도구   
Mocha와 Chai처럼 RSpec의 describe-it을 지원하며 expect로 단언(assertion) 할 수 있다.

(Jest 처음 접해보았다.)   

* 참고하면 좋은 링크
    * [BETTER SPECS](https://www.betterspecs.org/)
    * [Ginkgo - Go 언어 개발자를 위한 BDD 테스팅 프레임워크](https://www.youtube.com/watch?v=gfTsSBRvdqI)
    * [JUnit5로 계층 구조의 테스트 코드 작성하기](https://johngrib.github.io/wiki/junit5-nested/)
    * [Let's RSpec](https://github.com/ahastudio/til/blob/main/ruby/20161206-rspec-let.md)
    * [Given-When-Then](https://megaptera.notion.site/Given-When-Then-c4b62b46710942a181a6d477e502e458)

링크들을 한번 다 둘러보았는데 사실 봐도 잘 모르겠다..

### 기본적인 테스트 코드와 BDD 스타일

* 기본적인 테스트 코드
```
test('무엇을 테스트할 지 작성',()=>{
    expect(add(1,2)).toBe(3);
    // expect(함수).toBe(결과) 로 진행이되며
    // expect의 결과와 toBe의 값이 같으면 통과
})
```

* BDD 스타일의 테스트 코드 (이걸 이해하느라 강의를 3번봤다..)

```
describe('무엇에 대해 테스트할 지',()=>{
    it('그것에 대해 어떠한 테스트를 할지',()=>{
        expect(add(1,2)).toBe(3)
    })
})
describe('add 함수 테스트',()=>{
    it('add함수 두 숫자의 합',()=>{
        expect(add(1,2)).toBe(3)
    })
})
```

이해를 하고 나니 BDD 스타일이 조금 더 테스트 목적이라면 좋을 것 같다.   

context로 더 많은 예시? 문제? 에 대한 테스트도 진행 가능하다.

```
const context = describe;

describe('add 함수에 대한 테스트', () => {
	context('두 수가 양수로 주어졌을 때', () => {
		it('항상 숫자의 큰 값을 돌려줌', () => {
			expect(add(1, 2)).toBeGreaterThan(2);
			expect(add(1, 2)).toBeGreaterThan(1);
			// Add(1,2)의 리턴값이 3이므로 toBeGreaterThan(2),(1)
			// 의 2와 1보다 리턴값이 커서 테스트 통과
		});
	});
    context('하나는 양수 하나는 음수 일때',()=>{
        it('항상 하나의 양수보다 작은 값',()=>{
            expect(add(1,-2)).toBeLessThan(1);
        })
    })
});
```
하나의 함수에 대한 여러가지 조건들에 대한 테스트들을 진행해줄 수 있다.

## React Testing Library

[React Testing Library 공식문서](https://testing-library.com/docs/react-testing-library/intro/)   
[Jest-dom](https://testing-library.com/docs/ecosystem-jest-dom/)   

* UI에 특화된 라이브러리다. E2E Test 처럼 사용이 가능하다.
    * E2E (End to End) 테스트의 약자이며
    * 애플리케이션의 흐름을 처음부터 끝까지 테스트 하는걸 의미
* 단 "F/E 테스트 = only React 컴포넌트 테스트"가 되는 상황은 최대한 피하는게 좋다.
* 참고자료
    * [프론트엔드도 테스트해야 하나?](https://testing-library.com/docs/ecosystem-jest-dom/)
    * [Mocking 때문에 테스트 코드를 작성하기 어렵나?](https://www.youtube.com/watch?v=RoQtNLl-Wko&feature=youtu.be)

### 간단한 테스트 코드

```
test('Greeting 이라는 컴포넌트에 대한 검사', () => {
	render(<Greeting name='world'/>);

	screen.getByText('Hello, world!');
	// 화면에 정확히 Hello, world!를 찾아야 통과시켜준다.
	// 대소문자 구분과 특수문자도 체크함
	screen.getByText(/Hello/);
	// 정규식을 사용하여 일부만 체크할 수 있음

	screen.queryByText(/Hi/);
	// GetByText는 없으면 에러를 내주는데
	// query는 없으면 없는걸로 나온다.
});
```

* * *

### 테스팅 도구를 처음 접해본 결과..

너무나 어려웠다. 처음에 무슨 말인지도 이해가 되질않았고 강의만 3번 돌려보고 검색 또한 많이 해본 결과 하나씩 이해가 됐다.   
물론 100퍼센트 이해가 된건 아니겠지만 계속 사용해보며 이해를 해봐야겠다.