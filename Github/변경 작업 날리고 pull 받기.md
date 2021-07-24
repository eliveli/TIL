### 변경 작업 날리고 새로 pull 받아야 하는 상황

로컬의 내 개인 브랜치에서 원격의 마스터 브랜치를 pull 받았다. 
변경 사항을 반영하고 브랜치 이름 뒤에 ``` | MERGING``` 표시가 붙음.
그리고 중요하지 않은 작업을 하다가
마스터 브랜치가 업데이트 되어 새로 pull 받아야 했다.
pull 명령어를 사용하니 아래와 같은 문구가 뜸.
 ```
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)
  ```
병합되지 않은?  변경된 파일을 처리해야 한다는 것 같은데, 뭘 건드리기 조심스러웠다.
git stash를 이용하려 했는데, 이전에 stash를 한 번 해서 그런지 원하는 결과가 안 나옴.

### 내가 했던 방법(순차적으로)
1. 작업 되돌리기
```
git log
git reset  특정커밋
```
git log를 찍어본 후 복귀하고 싶은 작업의 commit 아이디를 가져와 git reset을 했다.
덕분에 이전 작업으로 돌아왔고.

그런데 추가된 파일이 남아 있기에 혹여 변경된 사항이 섞였나 싶어 다른 방법도 찾아 보았다.
```
git log
git reset --hard 특정커밋
```
```
git reflog
git reset --hard 특정커밋
```
...
이전으로 추가된 파일은 없애면서 작업을 완전히 되돌리는 법을 모르겠다.
그래도 작업이 되돌아갔으니 큰 문제는 없겠지 싶어
그냥 그 상태로 원격 master에 pull 받음.

블로그 글 참고!
https://medium.com/@kwoncharles/git-%EC%9D%B4%EC%A0%84-commit%EC%9C%BC%EB%A1%9C-%EB%8F%8C%EC%95%84%EA%B0%80%EA%B8%B0-cf6caed43ed5
https://88240.tistory.com/284
https://worthpreading.tistory.com/93

그런데 변경 사항을 빼 버리고 마스터 브랜치의 작업만 pull 받고 싶었다.
그래서 로컬 프로젝트 폴더의 내 브랜치를 삭제해 보았다.

2. 깃 로컬 브랜치 삭제하기. (필수는 아님...)
다른 브랜치로 이동 후
해당 브랜치 삭제.
```
git branch -d 브랜치 이름
```
https://gofnrk.tistory.com/99

그러나.. 여전히 변경 사항이 남아 있었던 것 같다.
그래서 새로운 폴더를 만들어 다시 pull 받아 옴.
아래 작업.

3. 새로운 폴더에 pull 받기

새로운 폴더에 git init,
변경 사항이 없으면 브랜치를 만들 수 없기에
파일 하나 만들어서 add, commit , branch 생성 및 이동,
이후 pull을 했더니 아래 에러가 뜸.
```fatal: refusing to merge unrelated histories```
그래서 아래 명령어로 pull을 받아옴.
```
git pull origin master --allow-unrelated-histories
```
https://www.educative.io/edpresso/the-fatal-refusing-to-merge-unrelated-histories-git-error

이후 package.json이 있는 폴더로 이동,
``` yarn install```,
 그리고 다시 작업....하.....

뭔가 할 필요 없는 작업을 빙 돌아서 한 건....아니겠지....ㅎ
그래도 여러가지 깃 명령어를 사용해 봄...

-2021.07.13-
