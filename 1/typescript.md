## TypeScript

### 학습 키워드

* REPL
* TypeScript
    + Interface vs Type
    + 타입 추론
    + Union Type vs Intersection Type
    + Optional Parameter

***

## REPL

    * REPL 사용하는 방법
        + npx ts-node

## TypeScript

* 간단한 타입 지정
    + 타입스크립트는 자바스크립트에서 타입을 확실히 잡아주는 느낌이다.

```
let name :string;

name = '김씨';
// name은 string으로 타입을 지정해두었으니 string 이외의
// 타입이 들어간다면 에러로 알려준다.
name = 13; // error

let age: number;

age = 16;

let human : {
    name: string;
    age: number;
};
human = {name: '김씨', age: 16};
```
간단히 타입을 확실하게 잡아준다. 라고 생각해주면 이해가 빠르다.   
그리고 자바스크립트엔 타입의 종류가 많다.   
number, string, null, boolean, object, array, symbol ... 등  

* 타입 정의하기 (타입 변수) / interface vs type
    + 복잡한 타입을 재사용하기 위해 타입을 변수처럼 만들 수 있다.
    + 나는 이걸 타입 변수라 부른다.
    + 함수의 매개변수에도 타입 지정이 가능하다.
    + 함수의 리턴값에도 타입 지정이 가능하다.

```
type Human = {
    name: string;
    age: number;
}

let boy: Human;

boy = {name : '홍길동', age : 13}
// 여기서 boy의 타입은 위에서 만들어 둔 Human 타입대로 잡힌다.

interface Person {
    name: string;
    age: number;
};

let girl: Preson;

girl = {name : '옥순이', age:36};

function add(x: number, y: number): number{
    return x + y
}
add(1,2);
add('1',2); // 에러
```

* 정해진 값과 배열 그리고 Tuple
    + 정해진 값의 경우는 const와 비슷한 느낌을 줄 수 있다.
    + 배열 타입 지정은 간단하다.
    + 배열을 좀 더 깐깐하게 관리할 때 사용하는게 Tuple

```
// 정해진 값을 타입으로 지정해주기
let category: 'food'
category = 'food';
// food 이외 다른것이 들어오면 에러로 잡아준다.

// 배열 타입과 tuple
let numbers: number[];
// 괄호 붙여주면 된다.

// tuple

let anythings: any[]; // 아무거나 들어올 수 있는 배열
anythings = ['hp',256];

let pair: [string, number]; tuple로 지정해둔 배열
pair = ['hp',256]
```

* 타입 추론
    + 타입 추론은 타입스크립트가 알아서 타입을 지정해주는 것이다.
    + 타입 추론이 있기에 모든것에 타입을 다 지정해줄 필요는 없다.

```
const name: string = '홍길동';

const haribo = '곰젤리';
// 둘 다 결국 string으로 타입스크립트가 알아서 타입을 지정해준다.
```

* Union Type
    + 여러 타입 중 하나를 사용하게끔 만든다.
    + boolean의 경우는 true | false

```
type bool = true | false;

let flag: bool;

flag = true;

flag = false;

flag = 3; // 에러 true와 false만 들어올 수 있다.

// 유용한 점은 매개변수에서 들어와야 할 값을 제한할 때

type Category = 'food' | 'toy' | 'bag';

function fetchProducts({category}: {category: Category}){
    console.log(`Fetch ${category}`);
}
// 매개변수 카테고리에는 food toy bag 만 들어갈 수 있다.

let target: string | number;

target = '홍길동';

target = 13;

target = null; 
// 에러 target의 타입은 string | number 둘 중 하나여야 함

target = undefined; // 에러 위와 같음

let targetName: string | undefined;

targetName = '홍길동';

targetName = undefined;

```

* Optional Parameter
    + 위 targetName 처럼 undefined를 쓸 일은 없다.
    + 물음표 기호(?)를 사용하여 Optional Parameter를 사용할 수 있음
    + 물음표 기호는 여러곳에 사용을 할 수 있다.

```
function greeting(name?:string): string{
    return `Hello, ${name || 'world'}`;
}
// 위 함수의 매개변수에는 name? 으로 Optional Parameter를
// 적용한 모습이다. 매개변수 name이 들어올 수도 안들어올 수도
// 있다 라는걸 알려준다. name이 없다면 world를 내줄것

// 기본값을 미리 지정해두면 좋다.
function greeting(name: string = 'world'): string {
    return `Hello, ${name}`;
}
// 매개변수에 아무것도 들어오지 않는다면
// 기본값인 world를 내준다.

// 매개변수가 객체일 때도 활용 가능하다.

function greeting({name, age}: {name: string; age?: number}): string{
    return age ? `${name} (${age})` :name;
}
// 매개변수에 age는 들어올 수도 안들어올 수도 있다.
```

* 타입 변수를 만들어주고  함수에 적용한 모습
    + 객체 타입 변수를 만들어줄 때도 물음표를 쓸 수 있다.
    + 객체에서 물음표는 이 옵션이 들어올 수도 안들어올 수도 있다 라는걸 알려준다.

```
type Human = {
    name: string;
    age?: number;
}
// age는 들어올 수도 안들어올 수도 있다.

function greeting({name,age}: Human): string{
    return age ? `${name} (${age})` : name ;
}

greeting(); // 필수로 받아야할 name이 없기에 에러가난다.
greeting({name: '홍길동'}); // 필수로 받을 name은 존재하고
// age는 있을 수도 없을 수도 있기에 에러는 나지않는다.
greeting({name: '홍길동', age: 13}) // 당연히 에러 안난다.

```

+ Intersection Type
    + 타입 합치기? 라고 생각할 수 있다.
    + 두가지의 타입을 하나로 묶어준다.
    + 두가지의 타입을 모두 만족 시켜야한다.

```
type Human = {
    name: string;
    age: number;
}
type Creature = {
    hp: number;
    mp: number;
}

type Person = Human & Creature;

let person: Person;
person = {name: '홍길동', age: 13, hp: 256, mp: 22};

// Person 타입은 Human과 Creature를 합쳤기에 모두 만족해줘야함

```

## 타입스크립트를 사용하는 이유

에러를 방지해주기 위해 타입스크립트를 사용하는것 만으로 알고있었으나 자동완성 및 실시간 오류 검사 등 사용하는데엔 여러 이유들이 존재한다.

***

### 봐두면 좋은 링크

[타입정의](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%ED%83%80%EC%9E%85-%EC%A0%95%EC%9D%98%ED%95%98%EA%B8%B0-defining-types)   
[type과 interface의 차이](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%ED%83%80%EC%9E%85-%EB%B3%84%EC%B9%AD%EA%B3%BC-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)   
[교집합](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes-func.html#%EA%B5%90%EC%A7%91%ED%95%A9)   
[Intersection Type](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)   
[Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)   
[Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)   
[좋은 타입스크립트 프로그래머로 만드는 11가지 팁](https://velog.io/@lky5697/11-tips-that-help-you-become-a-better-typescript-programmer)

***
