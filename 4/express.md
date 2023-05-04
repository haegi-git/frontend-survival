# Express

## 학습 키워드

* Express란?
* URL 구조
* REST API
* HTTP Method(CRUD)

* * *

### Express란?

[참고 자료](https://despiteallthat.tistory.com/139)

[공식 자료](https://expressjs.com/ko/)

Express는 Node.js를 위한 웹 프레임워크이다.

Express는 간단히 Node.js를 사용하여 쉽게 서버를 구성할 수 있게 만든 클래스와 라이브러리의 집합체

* Express설치, TS를 사용하기 위한 방법
  * 작업할 폴더를 만들어 준 뒤
  * 폴더를 터미널로 열어준 다음
  * `npm init -y` 입력 후 package.json 생성
  * .gitignore 파일 생성 후
  * 터미널에 `echo "/node_modules/" > .gitignore` (그냥 .gitignore 파일에 /node_modules/를 추가해도 된다.)
  * 타입 스크립트 설치 `npm i -D typescript` > `npx tsc --init` tsconfig.json 생성
  * tsnode 설치 `npm i -D ts-node` : 터미널에서 작업해볼 수 있다.
  * eslint 설치 `npm i -D eslint`  `npx eslint --init`
    * style, javascript, none, yes , Node, guide, xo, javascript, npm 순
  * express 설치 `npm i express` > `npm i -D @types/express`

순으로 설치해주면 된다.

### 설치에 관해서는 추후 나만의 세팅들을 블로그에 저장해두고 사용할 예정

### Express 사용 방법

일반 타입스크립트 사용하듯 app.ts를 생성 후 사용해주면 된다.

```ts
import express from 'express';

const port = 3000;

const app = express();

app.get('/', (req, res) => {
 res.send('Hello, world!');
});

app.listen(port, () => {
 console.log(`Server running at http://localhost:${port}`);
});
```

기본적인 모양이며 현재는 코드를 수정하고 저장을 했을 때 변경사항이 적용이되지않으며 서버를 재실행해줘야한다.

재실행하는 문제를 막아주기위해 nodemon을 사용한다.

`npm i -D ts-node` 를 꼭 해주어야 한다.

`npm i -D nodemon`

`npm nodemon app.ts`

`npx ts-node app.ts` ts-node로 실행하는 코드

package.json에 "start"를 추가해 "nodemon app.ts"를 추가해주면 npm start로 간단히 실행할 수 있다.

* * *

### URL 구조

[참고 자료](https://www.beusable.net/blog/?p=4507)

URL과 도메인은 다르며

도메인은 IP주소를 갖는 서버를 사용자가 쉽게 기억하고 찾을 수 있도록 만들어주는 서비스.

URL은 도메인을 포함한 경로 사용자가 도메인 서버로 접속할 때 프로토콜과 서비스타입을 통합적으로 적어준 것

간단한 개발할 때 localhost:3000 으로 접속할 때 주소창을 보면 간단히 localhost:3000만 나타나 있는걸 볼 수 있는데 요즘 크롬에서 저런식으로 보여주는 것일 뿐

실제로는 <http://localhost:3000/> 까지 나타나있는걸 알 수 있다.

* * *

### REST API

[참고 자료](https://velog.io/@paul7/Node.jsExpress-Express%EB%A1%9C-REST-API%EB%A5%BC-%EA%B0%9C%EB%B0%9C%ED%95%B4%EB%B3%B4%EC%9E%90)

[참고 자료](https://land-turtler.tistory.com/m/123)

벌써 두번째 등장하는 REST API이다.

REST의 구성요소로 Resource와 Verb가 있다.

Resource는 말 그대로 자원이며 서버는 유니크한 id값을 가지고있으며 (상품이라면 상품마다의 id값?), 그 id값을 클라이언트는 리소스에게 요청을 보내며

Verb는 행위이며 위 Resource, 자원을 가공하는 방법인 4가지 CRUD (Create, Read, Update, Delete)라고 부른다. 이 작업들을 REST API에서는 Method라 부르며 메소드는 HTTP의 method를 사용한다.

REST API를 사용하는 이유는 API의 목적이 무엇인지 명확하게 하기위해 사용한다.

### HTTP Method(CRUD)

REST API를 사용하여 HTTP Method,CRUD를 대입할 때

Create(생성) : POST

Read(읽기) : GET

Update(변경) : PUT(전체)/PATCH(일부)

Delete(삭제) : DELETE

로 사용하며 GET에 대한 예제로

```js
app.get('/products', (req, res) => {

 const products = [
  {
   category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
  },
  {
   category: 'Fruits', price: '$1', stocked: true, name: 'Dragonfruit',
  },
  {
   category: 'Fruits', price: '$2', stocked: false, name: 'Passionfruit',
  },
  {
   category: 'Vegetables', price: '$2', stocked: true, name: 'Spinach',
  },
  {
   category: 'Vegetables', price: '$4', stocked: false, name: 'Pumpkin',
  },
  {
   category: 'Vegetables', price: '$1', stocked: true, name: 'Peas',
  },
 ];
 
 res.send({ products });
});
```

app에 get요청으로 데이터를 읽어오는 예제라 이해할 수 있을 것 같다.

* * *

확실한건 REST API는 꽤나 자주 등장하며 내가 프론트엔드를 목표로 공부를 하고있다 해서 React만 공부할 건 아니다.

백엔드에 대한 지식도 어느정도 갖고있다면 좋을 듯 하다.

중간중간 이해가 되지않는다면 IT지식 책을 다시한번 정독해야할 것 같다.

Express는 전에도 한번 살짝 발만 담궈봤었는데 기회가된다면 한번 더 공부해보는것도 좋을 듯 하다.
