# Git-Command
Git 명령어를 작성합니다.

## Git 저장소를 clone 하기
clone을 원하는 디렉토리로 이동 후 명령어를 실행합니다.
```bash
$ git clone [clone git repository directory]
$ cd [clone directory root]
```

여기서 [clone git repository directory] 는 https://github.com/yuniithings/TIL.git이 되며,<br/>
[clone directory root]는 TIL 이 됩니다.

```bash
# exmaple
$ git clone https://github.com/yuniithings/TIL.git
$ cd TIL
```

### Git 저장소에 [Direcotry | File] 의 변경사항을 추가하기

```bash
$ git add [add directory | file]
```

여기서 [add directory | file]는 Git이 됩니다.<br/>
directory를 add할 경우 directory 하위에 파일이 존재해야 합니다.<br/>

아래의 예제코드는 폴더와 파일 생성 샘플까지 작성하였습니다.

```bash
# exmaple
$ mkdir Git
$ vi Git/README.md
```
vi editor의 `:wq` 명령어로 빈 파일을 저장후 vi editor를 종료합니다.<br/>

Git Repository에 새로운 변경사항을 추가합니다!
```bash
# example
$ git add Git
```

현재 Directory 및 하위의 Directory의 모든 변경사항을 추가하고 싶은 경우엔 어떡할까요?<br/>
위의 예제코드를 모두 번거롭게 실행할 필요가 없습니다!<br/>
```bash
$ git add .
```

현재 Directory 및 하위의 Directory의 모든 변경사항이 추가되었습니다.

```
이 항목들은 제가 조금 더 확인해볼게요.
`git add`명령어는 나의 Git Repository에 Create와 Delete가 일어났을 경우에만 사용합니다.
```
파일의 Update일 경우엔 Commit과 Push를 바로 사용할 수 있습니다. 그런데 Commit과 Push는 어떻게 사용하냐구요?<br/>
다음 항목에서 설명합니다.

## Git 저장소에 Commit 하기

`git add` 명령어로 추가된 항목들의 변경사항을 Commit 합니다.
```bash
$ git commit
```

Commit시 메시지를 작성할 때는 `-m` 옵션을 추가합니다.
```bash
$ git commit -m [message]
```

여기서 [message]는 Update README.md 가 됩니다.<br/>
주의할 점은 [message]는 항상 따옴표로 감싸주셔야 합니다.
```bash
# example
$ git commit -m "Update README.md"
```

## Git Push / Pull 하기

최초의 branch, master에 Commit한 사항들을 Push 합니다.
```bash
$ git push origin master
```

다른 branch에 Push하고싶다면 master를 다른 branch name으로 바꿔주세요!<br/>

신기하게 Push 명령어를 보니 Pull 명령어도 알것같네요.
```bash
$ git pull origin master
```

---
다음에 작성할 항목들이니 돌아가주세요.

## Git Commit Revert 하기

## Git Branch 생성하기

## Git Branch 변경하기

## Git Branch Merge 하기

## Git Branch CherryPick 하기
