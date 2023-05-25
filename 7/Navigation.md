# Navigation

## 학습 키워드

* Web APIs - History
* React Router - NavLink, Link, Navigate, useNavigate

* * *

### navigation

앞서 진행했을 때 a태그를 이용해 경로를 변경했었는데 a태그를 이용한 경로변경은 페이지 새로고침을 불러오며

페이지 새로고침은 리액트의 장점인 SPA를 제대로 사용할 수 없게된다. 자연스럽게 페이지 전환을 하기위해 리액트 라우터에 내장되어있는 기능을 사용한다.

기본적으로 Link,useNavigate를 많이 사용해봤었다.

* Link

```ts
<Link to="이곳에 주소를">메인</Link>
<Link to="/">메인</Link>
<Link to="/about">어바웃</Link>
```

Link의 기본적인 사용 모습은 a태그와 별 다를게없다. a태그와 똑같이 사용해주면 되고 Link를 사용해보면 새로고침 없이 페이지전환이 되는걸 볼 수 있다.

NavLink 태그도 존재하는데 NavLink의 경우 현재의 페이지에 액티브 클래스를 달아준다.

* NavLink

```ts
<NavLink to="이곳에 주소를">메인</NavLink>
<NavLink to="/">메인</NavLink>
<NavLink to="/about">어바웃</NavLink>
```

메인을 눌렀을 경우 메인에 active를 달아주고 어바웃을 눌렀을 경우 어바웃에 active를 달아준다. (아마 css를 추가해 현재의 페이지를 눈에 띄게 도움을 줄 수 있는 용이지 않을까 싶다.)

* Navigate

```ts
<Navigate to='/경로' />
```

위와 같이 사용을 해주면 밑도끝도없이 이동시켜버린다. (리다이렉션? 시켜버림)

[리다이렉트](https://webstone.tistory.com/65)

그러고 로그아웃 페이지를 테스트 진행시켜보면

```ts
context('여기는 로그아웃페이지', () => {
  it('리다이렉트 메인화면', () => {
   renderRouter('/logout');
   screen.getByText(/메인페이지/);
  });
 });
```

테스트가 에러가나는걸 볼 수 있는데 whatwg-fetch를 임포트해와서 해결해줘야한다.

npm i -D whatwg-fetch 설치 후 setupTests.ts 에서 import해오면 된다.

Navigate보다는 useNavigate를 더 많이 사용한다.

로그아웃 버튼에는 굳이 들어갔다가 돌아올 필요가 없다. 그렇기에 링크를 사용할 필요도없이 버튼으로 해결해주면 된다.

* useNavigate

```ts

const navigate = useNaviate();

const logoutBtn = () =>{
  navigate('/')
}

<button type='button' onClick={logoutBtn}>로그아웃</button>
```

위와 같이 사용을 해주면 버튼을 눌렀을 때 메인페이지로 돌아가는 걸 확인해볼 수 있다. (logoutBtn 함수에 로그아웃 기능까지 추가해주면 로그아웃이 완성이된다.)

* * *

### 마무리

마무리로 라우터에 관한건 종종 독학할때도 자주 사용을 했었기에 충분히 이해가 쉽게가긴했으나 객체로 사용하는 방법에 대해서는 낯설기에 이 부분에 있어서 조금 더 익숙해지려 해야할 것 같다.

객체로 사용하면 테스트에 좀 더 도움이 되는 듯 하니 나쁘지않을 것 같다.