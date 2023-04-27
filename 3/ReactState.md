# React State

## 학습 키워드

- React State란?
- DRY 원칙
- SSOT(Single Source of Truth)
- useState
- 1급 객체(first-class object)란?
- Lifting State Up

* * *

## React State란?

[공식 문서](https://ko.legacy.reactjs.org/docs/faq-state.html)

state란 리액트에서 이벤트에 의해 변경되는 동적인 값

쉽게 생각해서 나는 변경되는 데이터, 변수 라고 생각한다.

react에서 state를 사용할 땐 useState를 사용한다.

React State의 조건으로

1. 변경되야한다. 변경되지않는건 state로 다룰 가치가 없다.
2. 부모 컴포넌트가 props를 통해 전달한다면 state가 아니다.
3. 다른 state나 props를 이용해 계산 가능하다면 state가 아니다.

아무렇게 만들어도 되지만 가능한 DRY원칙을 따르라고한다.

* * *

## DRY 원칙 (중복 배제 원칙)

[위키피디아](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
[참고 자료](https://kim-dragon.tistory.com/256)

똑같은 일을 두번 반복하지 말 것

DRY를 지켜준다면

- 코드가 단순해지며 한번만 작성할 수 있다
- 한 곳에서만 코드를 변경하고 모든 인스턴스들에서는 변경사항만 확인할 수 있다.
- 시간과 노력이 절약되고 유지보수가 쉬우며 버그 가능성도 줄여준다.

DRY 원칙 위반

- 같은 코드나 로직을 반복해 작성하거나 복사하여 붙여넣기 하는 행위

* * *

## SSOT(Single Source of Truth)

[참고 자료](https://www.lesstif.com/software-engineering/ssot-single-source-of-truth-128122887.html)

단일 진실 공급원이란 정보 시스템 설계 및 이론 중 하나로 정보와 스키마를 오직 하나의 출처에서만 생성 또는 편집하는 방법론이다.

이 방법은 알게 모르게 해왔었을 수도 있고 작업을 진행하다보면 이 방식을 사용하게 될 것 같다.

* * *

## useState

useState는 리액트에서 state를 다루기 위해 사용하는 도구이다.

```react
const [data,setData] = useState(0)
```

위와 같은 모양으로 사용한다.

변수 처럼 생각하면 쉽다. data라는 state에 0이라는 값을 넣어준 것

state의 값을 변경하기 위해서는 뒤에 지정해준 setData를 사용해주면 된다. 간단히 변경함수라 생각해주면 된다.

```react
setData(1)
```

위와 같이 사용해주면 data에 들어있던 0이 1로 변경시켜줄 수 있다.

react를 사용한다면 state는 항상 사용을할테니 금방 익숙해질 것

* * *

## 일급 객체(First Class Object)란?

[참고 자료](https://velog.io/@reveloper-1311/%EC%9D%BC%EA%B8%89-%EA%B0%9D%EC%B2%B4First-Class-Object%EB%9E%80)

[참고 자료](https://developer-cheol.tistory.com/42)

1급 객체의 조건

- 변수나 데이터에 할당할 수 있어야 한다.
- 객체의 인자로 넘길 수 있어야 한다.
- 객체의 리턴값으로 리턴 할 수 있어야 한다.

1급 객체라는걸 처음 들어봤기에 참고 자료를 좀 더 둘러보고 알아봐야 할 것 같다.

* * *

## Lifting State Up

[참고 자료](https://velog.io/@devjade/React-State-%EB%81%8C%EC%96%B4%EC%98%AC%EB%A6%AC%EA%B8%B0Lifting-State-Up)

[예제 참고 자료](https://nychicken.tistory.com/9)

React는 단방향 데이터 흐름을 갖고 있다. 앞 컴포넌트에서 props를 메모할 때 props는 부모 컴포넌트에서 자식 컴포넌트에게 넘겨주는 방향으로만 작동된다.

이와 같은 방식을 단방향 데이터 흐름이라하는데 이 단방향 흐름 원칙에 부합하는 해결 방법이 Lifting State Up(상태 끌어올리기)이다.

* * *

이번에는 처음 들어본 것이 꽤나 있었기에 찾아보고 공부하는데 조금 헤맸다. 상태 끌어올리기나 SSOT, DRY, 1급 객체 모두 처음 들어보는 키워드였고 알아보니 독학을 하며 자연스레 사용하던 것도 있었고 꽤나 복잡한 이론도 있었던 것 같다. 모든걸 외우기엔 벅찰 수 있으니 공부를 하며 자연스레 익히는 것이 좋을 듯 하다.