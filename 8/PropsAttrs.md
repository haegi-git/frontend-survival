# Props와 Attrs

## 학습 키워드

* props
* attrs

* * *

### Props

스타일드 컴포넌트에서는 props를 사용할 수 있다.

일반 컴포넌트에서 props를 받아서 사용하듯 사용할 수 있는데 이걸 활용해 토글버튼, 어떤 상태일때 어떠한 스타일을 넣을 수 있는 용도로 사용이된다. 기본적인 사용방법으로 커스텀 훅인 useBoolean을 사용한 예제를 보면

```js

type ButtonProps = {
    active: boolean;
}

const Button = styled.button<ButtonProps>`
    background-color: ${props => props.active ? '#00F' : '#FFF'};
 font-size: 40px;
    color: ${props => props.active ? '#FFF' : '#000'};
    border: 1px solid #888;
`

export default function Switch(){
    const {value: active, toggle} = useBoolean(false);

    return(
        <Button 
        active={active} 
        onClick={toggle} 
        type='button'>토글버튼</Button>
    )
}

```

위 와 같이 사용을 해주면 클릭할 때 마다 배경색상과 글자 색이 변하는걸 볼 수 있다. props로 상태값을 받아와 사용하는 styled components 사용방법은 자주 사용되며 여러방면에서 활용되니 손에 익혀두면 좋다.

* * *

### attrs

attrs를 사용하면 속성값을 미리 지정해줄 수 있다.

button의 경우 type 속성을 미리 잡아주는 데 사용해줄 수 있다.

```js
type ButtonProps = {
 type?: 'button' | 'submit' | 'reset';
 active?: boolean;
};

const Button = styled.button.attrs<ButtonProps>(props => ({
 type: props.type ?? 'button',
}))<ButtonProps>`
    background-color: ${props => props.active ? '#00F' : '#FFF'};
 font-size: 40px;
    color: ${props => props.active ? '#FFF' : '#000'};
    border: 1px solid #888;
`;

export default function Switch() {
 const {value: active, toggle} = useBoolean(false);

 return (
  <Button
   onClick={toggle}
   active={active}>on/off</Button>
 );
}
```

이 경우 styled components를 만드는 Button에 타입을 두번 잡아줘야한다 attrs에 한번 button에? 한번,

위 처럼 사용할 경우 Button에 직접 type을 집어넣어 submit을 만드는게 아닌 이상 type이 비어있다면 기본적으로 button을 넣어준다.

미리 만들어둔 Button의 스타일을 거의 그대로 사용하면서 다른 스타일을 덮어쓰는 방법은

```js
type ButtonProps = {
 type?: 'button' | 'submit' | 'reset';
 active?: boolean;
};

const Button = styled.button.attrs<ButtonProps>(props => ({
 type: props.type ?? 'button',
}))<ButtonProps>`
    background-color: ${props => props.active ? '#00F' : '#FFF'};
 font-size: 40px;
    color: ${props => props.active ? '#FFF' : '#000'};
    border: 1px solid #888;
`;

const PrimaryButton = styled(Button)`
    background-color: ${props => props.active ? 'red' : 'green'};
    font-size: 40px;
    color: ${props => props.active ? '#purple' : '#orange'};
    border: 1px solid #888;
`

export default function Switch() {
 const {value: active, toggle} = useBoolean(false);

 return (
  <PrimaryButton
   onClick={toggle}
   active={active}>on/off</PrimaryButton>
 );
}
```

위 처럼 styled(기존버튼) 을 넣어서 새롭게 지정해주면 나머지 옵션은 그대로이며 변경한 배경색과 글자색만 변경하는것도 가능하다.