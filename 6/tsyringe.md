# TSyringe

## 학습 키워드

* TSyringe
* 의존성 주입 (Dependency Injection)
* refliect-metadata
* sington (싱글톤)

* * *

### TSyringe?

[참고 자료](https://velog.io/@moongq/Dependency-Injection)

TSyringe는 자바스크립트와 타입스크립트 기반의 의존성 주입 컨테이너 라이브러리이다. 의존성 주입은 소프트웨어 디자인 패턴 중 하나로 객체 사이의 의존성을 외부에서 주입하여 결합도를 낮추고 유연성을 높이는걸 목표로 한다.

타입스크립트용 DI도구이며 External Store를 관리하는데 활용할 수 있다. 또한 Prop Drilling

Prop Drilling 사진
![Prop Drilling](https://react.dev/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fpassing_data_prop_drilling.png&w=640&q=75)

Prop Drilling은 props를 하위 컴포넌트로 전달하는 용도로 쓰이는 컴포넌트들을 거치며 React Components 트리의 한부분에서 다른 부분으로 데이터를 전달하는 과정을 말한다.

사진에서 보다시피 우측 가장 아래에서 최상위 컴포넌트의 데이터를 받아서 사용하려면 여러개의 컴포넌트를 거쳐와야한다.

### 의존성 설치

의존성을 설치해주고

```bash
npm i tsyringe reflect-metadata
```

src/main.tsx 파일과 src/setupTests.ts 파일에서 reflect-metadata 임포트 해준다.

```js
import 'reflect-metadata';
```

src/stores 폴더 생성 후 Store.ts 생성

```js
import { singleton } from 'tsyringe';

@singleton()
export default class Store{
    count = 0
}
```

Store를 사용할곳에 가져다 사용한다.

```js
import { container } from 'tsyringe';

import useForeceUpdate from '../hooks/useForceUpdate';

import Store from '../stores/Store';

export default function Counter(){
    const store = container.resolve(Store);

    const handleClick = () =>{
        store.count += 1;
        forceUpdate();
    }

    return(
        <div>
        <p>{store.count}</p>
        <button type="button" onClick={handleClick}>Increase</button>
        </div>
    )
}
```

@singleton() 에서 에러를 내주는걸 막기위해 tsconfig.json에서 Decorators 속성을 주석 해제해줘야한다.

스토어에서 만든 카운트를 화면에 렌더하며 스토어에서 만든 카운트를 +1 해주는 버튼의 기능을 만들어주면 제대로 정상 작동 하는걸 볼 수 있다.

다른 예시 또한 이해를 해보자.

```js

import { container } from 'tsyringe';

import useForeceUpdate from '../hooks/useForceUpdate';

import Store from '../stores/Store';

export default function CountControl(){
    const store = container.resolve(Store);

    const handleClick = () =>{
        store.count += 1;
        forceUpdate();
    }

    return(
        <div>
        <p>{store.count}</p>
        <button type="button" onClick={handleClick}>Increase</button>
        </div>
    )
}
```

Counter에서는 store.count += 1 코드를 제거해둠

```js
// Counter
import { container } from 'tsyringe';

import useForeceUpdate from '../hooks/useForceUpdate';

import Store from '../stores/Store';

export default function Counter(){
    const store = container.resolve(Store);

    const handleClick = () =>{
        forceUpdate();
    }

    return(
        <div>
        <p>
        Count :
        {' '}
        {store.count}</p>
        <button type="button" onClick={handleClick}>Refresh</button>
        </div>
    )
}
```

App.tsx에서 Counter와 CountControl을 둘 다 띄워준 뒤 테스트 해보면 CountControl에 있는 Increase버튼을 누르면 숫자가 즉시 업데이트되며 숫자가 증가하는걸 볼 수 있는데 Counter의 숫자는 리렌더링이 되지않으며 숫자가 증가하지않고 리프레시를 해줄 때 업데이트가 일어나는걸 볼 수 있다.

항상 리프레시를 눌러서 업데이트를 시켜줄 순 없다. 그렇기에 스토어 코드를 조금 수정해주면 된다.

```js
// Store.ts

import { singleton } from 'tsyringe';

@singleton()
export default class Store{
    count = 0

    forceUpdate: () => void;

    update(){
        this.useForceUpdate();
    }
}

```

스토어 코드를 수정해준 뒤 Counter와 CountControl도 변경해준다.

```js

import { container } from 'tsyringe';

import Store from '../stores/Store';

export default function CountControl(){
    const store = container.resolve(Store);

    const handleClick = () =>{
        store.count += 1;
        store.forceUpdate();
    }

    return(
        <div>
        <p>{store.count}</p>
        <button type="button" onClick={handleClick}>Increase</button>
        </div>
    )
}
```

Counter에 forceUpdate에 useForceUpdate()를 담아두고 store에 forceUpdate로 사용을 함 (Store에는 forceUpdate가 빈 함수로 되어있고 그걸 Update로 사용하는 모습?)

```js
// Counter
import { container } from 'tsyringe';

import useForeceUpdate from '../hooks/useForceUpdate';

import Store from '../stores/Store';

export default function Counter(){
    const store = container.resolve(Store);

    const forceUpdate = useForceUpdate();

    store.forceUpdate = forceUpdate;
    return(
        <div>
        <p>
        Count :
        {' '}
        {store.count}</p>
        </div>
    )
}
```

똑같이 업데이트된다.

근데 여기서 이제 App에서 Counter를 두개를 만들었을 때는 하나의 숫자만 올라간다. 그걸 또 고쳐주기 위해 코드를 변경해줘야한다.

```js
// Store.ts

import { singleton } from 'tsyringe';

type ForceUpdate = () => void;

@singleton()
export default class Store{
    count = 0

    forceUpdates: new Set<ForceUpdate>()

    update(){
        this.forceUpdates.forEach((forceUpdate) = {
            forceUpdate();
        });
    }
}

```

```js

import { container } from 'tsyringe';

import Store from '../stores/Store';

export default function CountControl(){
    const store = container.resolve(Store);

    const handleClick = () =>{
        store.count += 1;
        store.update();
    }

    return(
        <div>
        <p>{store.count}</p>
        <button type="button" onClick={handleClick}>Increase</button>
        </div>
    )
}
```

카운트컨트롤에는 store.update()를 사용하게끔 변경하고 카운터에는 forceUpdates.add(forceUpdate)를 넣어주면 둘 다 한번에 업데이트가 된다.

```js
// Counter
import { container } from 'tsyringe';

import useForeceUpdate from '../hooks/useForceUpdate';

import Store from '../stores/Store';

export default function Counter(){
    const store = container.resolve(Store);

    const forceUpdate = useForceUpdate();

    useEffect(()=>{
        store.forceUpdates.add(forceUpdate);

        return () => {
            store.forceUpdates.delete(forceUpdate);
            // 화면에서 사라졌을 때
        }
    },[store, forceUpdate])

    return(
        <div>
        <p>
        Count :
        {' '}
        {store.count}</p>
        </div>
    )
}
```

* * *

### 마무리

tsyringe로 검색했을 때 자료가 별로 나오지않았다. GPT에 물어봤을 땐 의존성 주입이라 알려주며 디자인 패턴에 일종이라 알려주었다.

강의에서 사용하는 모습을 보았을 땐 상태관리에 사용하는 도구라고만 느껴졌다. Redux를 사용하는 것과 같은 느낌으로

강의가 100퍼센트 이해가 되지않았으며 이해가 될 듯 하면서 코드를 점점 변경시킬 때 마다 이해가 되지않았다 ..

일단은 이정도로만 이해하고 사용방법에 대해서도 이정도로만 이해하고 넘어가자.. 내가 이해한 것처럼 상태관리에 관한 도구라면 리덕스에 더 집중을 해도 좋지않을까?