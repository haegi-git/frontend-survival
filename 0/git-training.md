---
description: 깃 사용방법 연습하기
---

# git training

1. 과제는 Pull Request를 보내 제출한다. fork하여 내 깃허브에 같은 repository를 생성한다. 그리고 SSH 주소를 복사하여 로컬 환경에서 터미널로 프로젝트를 클론해준다.
2. 터미널에서 clone하여 프로젝트를 내 컴퓨터 또는 노트북에 생성해준다.\
   (명령어 git clone 1번에서 복사한 주소 : git clone git@github.com:haegi-git/git-training.git)
3. bash의 경로를 지정해준다. (명령어 cd 경로 : cd git-training)\
   upstream 명령어로 PR 보낼 repository의 주소를 추가한다.\
   (명령어 remote add upstream 보낼 원격 주소)
4. 원격 저장소가 제대로 추가되었는지 확인한다. (명령어 git remote -v) \
   오리진에 내 주소가 있고 upstream에 보낼 곳 주소가 있다.
5. upstream 원격 저장소의 최신 상태를 반영해준다.\
   (명령어 git fetch upstream / git rebase upstream/main)
6. 새 브랜치를 생성해준다. (여기서 브랜치의 이름은 나의 깃허브 유저이름으로 생성)\
   (명령어 git switch -c 브랜치이름 upstream/main)
7. 1번에서 clone하여 내 컴퓨터에 생긴 파일들로 작업을 해준다. vsc로 불러와서 작업을 해주었다.
8. 작업을 해주었으면 변경된 점을 커밋 (명령어 git add . / 변경된 점 모두 추가)\
   (명령어 git commit / 커밋 git commit -m "메모" 내가 알던 커밋)
9. origin 원격 저장소에 작업 브랜치 올리기 (명령어 git push origin 브랜치 이름)
10. 과제 레포지토리를 들어가면 Compare & pull request 가 나타나는데 PR해주면 된다.

git을 많이 사용해보지 않았기에 조금 어려웠음..

