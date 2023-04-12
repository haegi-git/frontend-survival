## Parcel & ESLint

### 학습 키워드
* Bundler(번들러)
    * Parcel
* Lint(린트)
    * ESLint

* * *

### Parcel
[Parcel 공식문서](https://parceljs.org/)   

Zero Configuration
* 특별한 설정 없이 바로 사용 가능한 빌드 도구. 내부적으로 SWC를 적용해 기존 도구보다 빠르다. (ES Module을 적극 활용하는 Vite도 빠름)
    * 참고 자료
    * [Parcel](https://github.com/ahastudio/til/tree/main/parcel)
    * [Vite](https://github.com/ahastudio/til/tree/main/vite)

설정은 따로 필요없지만 두가지 작업은 해주자

* package.json 파일에 source 속성 추가
    
```
"source": "./index.html",
```

* 그리고 parcel-reporter-static-files-copy 패키지 설치

```
npm install -D parcel-reporter-static-files-copy
```

* .parcelrc 파일 생성 후 작성

```
{
  "extends": ["@parcel/config-default"],
  "reporters":  ["...", "parcel-reporter-static-files-copy"]
}
```

위 패키지 설치와 parcelrc 파일을 생성 해주면 static 폴더의 파일을 정적 파일로 serving 가능하다. (이미지 등 Assets)

* 빌드 + 정적 서버 실행
    * npm parcel build
    * npm servor dist

parcel을 사용하여 배포 전 미리 확인을 해볼 수 있다. (배포 전 테스트?)

* * *

### ESLint

[ESLint 공식문서](https://eslint.org/)   
[정적 프로그램 분석](https://ko.wikipedia.org/wiki/%EC%A0%95%EC%A0%81_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8_%EB%B6%84%EC%84%9D)   

ESLint를 사용하는 이유

* 코드 스타일을 통일해줄 수 있다.
* 잠재적 문제를 발견해줄 수 있다.
* 베스트 프랙티스 추천을 해준다. (최신 트렌드 학습에 도움이 된다.)

### ESLint 추가 세팅

* .vscode 폴더 생성 후 settings.json 파일을 추가

```
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
```
설정 해주면 저장시 바로 ESLint를 실행하여 코드를 수정해준다.

```
"trailing-spaces.trimOnSave": true
```
아래 위 속성도 넣어주면 도움이 될 것 같다. (마지막 줄 제거)

그리고 빌드 시 console.log를 제거해주어야하는데 그거에 관해서 알려주는 속성도 있다. 알아보면 좋을 것 같은 옵션이다.