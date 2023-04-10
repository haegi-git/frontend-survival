## 개발 환경 세팅
* * *

### Node.js

기본적으로 node.js를 기반이다. 수업에서는 더 간단한 deno 라는게 있다고 하였지만 처음 들어보는지라 추후 나중에 검색으로 구경이나 해봐야겠다.

### node.js는 항상 최신으로 받아두자
- 노드의 버전 앞 숫자가 짝수면 LTS 홀수면 최신이다.
- 항상 LTS를 사용했기에 LTS를 사용하기로했다.
- 여러 강의에서도 들었지만 대다수의 에러는 node가 최신이 아니라서 에러가 나는경우가 많다.

## 본격적으로 세팅하기

// cmd는 windows terminal 사용

    * mkdir 폴더이름 (폴더생성 명령어)
    * cd 폴더이름 (폴더 경로이동 명령어)
    * code . (vsc 열기, 나는 그냥 파일클릭해서 열었다.)

### 작업폴더를 생성해주었으니 vsc에서 열어주자
    
    * 작업할 폴더를 vsc 작업영역에서 띄워준 뒤 터미널 오픈
    * npm init -y (여기서 -y는 모두 yes해달라는 뜻)
        + 그리고 잊지말고 .gitignore 파일 만들어주기
        + 불필요한 파일 또는 폴더들 까지 커밋되는걸 막아준다.
        + [github gitignore 설정]: https://github.com/github/gitignore/blob/main/Node.gitignore

### 타입스크립트 설정

    * npm i -D typescript
    * npx tsc --init
        + tsconfig.json 파일이 생성이될텐데 그 중 
        주석처리된 jsx 속성의 주석을 해제해주자

### ESLint 설정

    * npm i -D eslint
    * npx eslint --init
        + .eslintrc.js 파일의 env 속성안에 jest: true를 추가
    * 여기서도 .eslintignore 파일을 생성해주자.
        + .gitignore와 똑같이 설정해줘도 상관없음

### 리액트 설치

    * npm i react react-dom
    * npm i -D @types/react @types/react-dom

### 테스팅 도구 설치

    * npm i -D jest @types/jest @swc/core @swc/jest \
    jest-environment-jsdom \
    @testing-library/react @testing-library/jest-dom
        + 나는 위 코드 복사해서 사용하니 에러나서 한줄로 쭉 쳤다.
    * npm i -D jest @types/jest @swc/core @swc/jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom
        + 문제가되는진 잘 모르겠다..
        + jest.config.js 파일을 생성준다.
        + 테스트에서 SWC를 사용할 수 있게 설정해두면 된다.

### Parcel 설치

    * npm i -D parcel
        + package.json 파일을 조금 수정해준다.

* * *

## 여기까지가 세팅 및 설치 끝

독학을 하면서 이렇게까지 설정을 하고 작업을 해본적이 한번도 없었다.   
그저 해본거라곤 확장도구에서 prettier 정도..?   

eslint를 이런식으로 사용을 처음해봤는데 npm run lint를 사용했을 때   
빨간 밑줄이 다 사라지는게 되게 기분이 좋았다...

또한 리액트도 항상 create-react-app 폴더이름   
이런식으로 생성해주는 방식을 사용해왔었는데   
이렇게 하나씩 직접 설치하고 세팅하는건 처음이어서   
꽤 번거로움을 느꼈다.. 나중에는 좀 더 편리하게 생성할 수 있을까?

더 좋은 세팅이 있는지도 알아보면 좋을듯하다.   
지금은 npm run lint를 사용할 때 열어둔 서버를 닫아야하는게  
번거로운데 저장과 동시에 처리해줄 방법이 있을까..
(밑줄이 거슬려..)