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

    *