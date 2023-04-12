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

### 폴더 생성

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

<details>
<summary>jest.config.js</summary>
    
```
    jest.config.js
    module.exports = {
	testEnvironment: 'jsdom',
	setupFilesAfterEnv: ['@testing-library/jest-dom/extend-expect'],
	transform: {
		'^.+\\.(t|j)sx?$': [
			'@swc/jest',
			{
				jsc: {
					parser: {
						syntax: 'typescript',
						jsx: true,
						decorators: true,
					},
					transform: {
						react: {
							runtime: 'automatic',
						},
					},
				},
			},
		],
	},
	testPathIgnorePatterns: ['<rootDir>/node_modules/', '<rootDir>/dist/'],
};

```

</details>

### Parcel 설치

    * npm i -D parcel
        + package.json 파일을 조금 수정해준다.
<details>
<summary>package.json</summary>

```
{
  "name": "frontend-survival-week01",
  "version": "1.0.0",
  "description": "이름 설명",
  "source": "index.html",
  "scripts": {
    "start": "parcel --port 8080",
    "build": "parcel build",
    "check": "tsc --noEmit",
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
    "test": "jest",
    "coverage": "jest --coverage --coverage-reporters html",
    "watch:test": "jest --watchAll"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@swc/core": "^1.3.49",
    "@swc/jest": "^0.2.24",
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^14.0.0",
    "@types/jest": "^29.5.0",
    "@types/react": "^18.0.34",
    "@types/react-dom": "^18.0.11",
    "@typescript-eslint/eslint-plugin": "^5.58.0",
    "@typescript-eslint/parser": "^5.58.0",
    "eslint": "^8.38.0",
    "eslint-config-xo": "^0.43.1",
    "eslint-config-xo-typescript": "^0.57.0",
    "eslint-plugin-react": "^7.32.2",
    "jest": "^29.5.0",
    "jest-environment-jsdom": "^29.5.0",
    "parcel": "^2.8.3",
    "process": "^0.11.10",
    "typescript": "^5.0.4"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  }
}
```

</details>

## ESLint Auto fix

    * vsc에서 컨트롤 + ,을 눌러 설정창 열기
    * 설정에서 auto fix on save 가 있으면 체크 auto fix on save가 없으면 넘어가기
    * 컨트롤 + , 눌러 설정을 열어준 뒤 code Actions on save를 검색
    * 여기서 Editor : Code Actions On Save의 settings.json을 편집해준다.

```
"editor.codeActionsOnSave": {
    
    "source.fixAll.eslint": true
},
  "editor.formatOnSave": true,
  ```
    * 위 설정을 추가해준다.
    * 그리고 다시 설정창을 열어서 formatter 검색 후 
    Enables ESLint as a formatter 체크해주면 끝

* * *

## 설정을 모두 끝내고

좀 더 다른 설정도 추가하면 좋겠지만 아직은 무엇이 더 있는지 잘 모르기에 이정도의 설정에 익숙해져도 좋을 것 같다.