# Styled-components

## 학습 키워드

* styled-components

* * *

### styled-components?

[공식 문서](https://styled-components.com/docs/basics)

앞서 말했듯 styled-components는 css-in-js를 사용하기 위한 라이브러리이며 나타난 이유는 앞 css-in-js에 작성이 되어있다.

* 설치

```bash
npm i styled-components
npm i -D @types/styled-components @swc/plugin-styled-components
```

``.swcrc`` 파일 생성 후

```json
{
 "jsc": {
  "experimental": {
   "plugins": [
    [
     "@swc/plugin-styled-components",
     {
      "displayName": true,
      "ssr": true
     }
    ]
   ]
  }
 }
}
```

* 간단하게 사용방법을 알아보면

```js

const Button = styled.button`
    font-size : 550px;
    color : blue;
`

return(
    <Button>버튼</Button>
)
```

위 와 같은 느낌으로 사용해주면 된다. 버튼이라는 스타일 컴포넌트를 생성해준 것이고 CSS를 적용해준 것

이 외에도 다양한 방법으로 사용해줄 수 있다.

위 버튼 스타일드 컴포넌트를 만들어 준 것에 추가로 스타일을 입혀줄 수도 있다.

```js

const SmallButton = styled(Button)`
    font-size : 100px;
`

return(
    <SmallButton>작은버튼</SmallButton>
)
```

폰트 색상은 그대로 두고 폰트 사이즈만 변경한 스타일을 입힌 모습이며

기존 컴포넌트에 스타일을 입히는 것도 가능하지만 기존 컴포넌트가 Class를 잡아줘야하는 점 주의

```js

function HelloWorld({className}: React.HTMLAttributes<HTMLElement>){
    return(
        <p>Hello, World</p>
    )
}

const Greeting = styled(HelloWorld)`
    color: #00F;
`

export default Greeting

```

등 여러가지 방법으로 사용할 수 있다.
