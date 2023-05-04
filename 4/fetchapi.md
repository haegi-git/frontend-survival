# Fetch API & CORS

## 학습 키워드

* Fetch API란
* Promise
* ReadableStream
* Unicode
* CORS란

* * *

### Fetch API란

Fetch 메서드는 자바스크립트에서 서버와 네트워크 요청을 보내고 응답을 받을 수 있게 해주는 메서드이다.

fetch API는 특정 URL로부터 정보를 받아오는 역할

AJAX로 많이 예시를 들어주며 js만으로 API를 받아올 때 경험해봤을 수 있을 것 같다.

* * *

### Promise

fetch 메서드를 사용해 데이터를 받아오면 Promise 상태로 받아오게된다.

그말은 즉 비동기 상태라는걸 의미한다.

fetch(받아올 데이터URL) 상태로 사용해보면 Promise로 pending 상태인걸 볼 수 있다.

Promise상태이므로 .then을 사용해 받아오는걸 성공 했을 때의 코드를 넣어줄 수 있고 await을 사용해도된다.

* * *

### ReadableStream

[MDN문서](https://developer.mozilla.org/ko/docs/Web/API/Streams_API/Using_readable_streams)

[MDN문서](https://developer.mozilla.org/ko/docs/Web/API/ReadableStream)

ReadableStream을 잘 사용할수록 자바스크립트 개발자로서 네트워크로 받은 데이터 스트림을 청크 단위로 읽고 다루는데 매우 유용하다고 한다.

크롬에서 fetch body 객체를 스트림으로서 사용할 수 있고 custom ReadableStream을 만들 수 있다.

Stream API의 ReadableStream 인터페이스는 바이트 데이터를 읽을 수 있도록 스트림을 제공하며 Fetch API는 Response 객체의 body 속성을 통해 ReadableStream의 구체적인 인스턴스를 제공

### 기본적인 사용법

```js
fetch('http://localhost:3000/products');
// → Promise

await fetch('http://localhost:3000/products');
// → Response

const response = await fetch('http://localhost:3000/products');
// → response.body는 ReadableStream

const reader = response.body.getReader();

const chunk = await reader.read();
// → chunk.value는 Uint8Array 타입.
// → 원래는 chunk.done이 true일 때까지 반복해야 한다.

const body = new TextDecoder().decode(chunk.value);

const data = JSON.parse(body);
```

정리를 하자면 ReadableStream은 읽을 수 있는 데이터 스트림이며 데이터의 크기가 크거나 서버에서 지속적인 업데이트되는 데이터 처리에 유용하다. ReadableStream을 사용하면 큰 데이터를 다운로드 하는동안 브라우저가 중단되지 않고 메모리 절약이 가능하다. (GPT)

또한 위 방식은 결국 최종적인 data값으로 JSON data를 받아오는데 기본적으로 JSON을 지원한다.

```js
const response = await fetch('http://localhost:3000/products');
const data = await response.json();
```

위 코드 만으로 똑같이 JSON 데이터로 받아올 수 있다.

다른 메소드를 사용하고싶다면

```js
const response = fetch(url, {
 method: 'POST',
});
```

url 뒤에 중괄호로 사용해주면 된다.

* * *

### CORS란

[MDN 공식](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)

[참고 자료](https://escapefromcoding.tistory.com/724)

CORS(Cross-Origin Resource Sharing) 출처가 다른 자원들을 공유한다 라는 뜻으로 다른 출처의 자원에 접근할 수 있는 권한을 부여하도록 브라우저에게 알려주는 체제이며

예시로는

<https://domain-a.com> 에서 XML을 이용하여 <https://domain-a.com/data.json>을 요청하는 경우이다.

CORS를 사용하는 요청에는

1. XML과 Fetch API 호출이 있고
2. 웹 폰트 (CSS 내 @font-face에서 교차 도메인 폰트 사용시)
3. WebGL 텍스처
4. drawImage() (en-US)를 사용해 캔버스에 그린 이미지/비디오 프레임.
5. 이미지로부터 추출하는 CSS Shapes. (en-US)

이 있는데 1번과 2번을 제외한 나머지는 사실 잘 모르겠다.

### Express에서 CORS 사용할 땐 미들웨어 설치하면 된다

패키지 설치

```bash
npm i cors
npm i -D @types/cors
```

CORS 미들웨어 사용

```js
import express from 'express';
import cors from 'cors';

const app = express();

app.use(cors());
```

CORS 미들웨어를 사용할 경우 Express에서 다른 경로의 데이터를 받아와도 에러가나지않는걸 볼 수 있다.