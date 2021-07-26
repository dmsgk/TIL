

# 자주 사용하는 Git 명령어

## 1. 되돌리기

### 원격저장소에 올려둔 상태로 프로젝트 되돌리기

- ```bash
  git fetch --all
  git reset --hard origin/main
  ```

- 아니면 `git checkout .`

### git add 되돌리기

- `git reset HEAD <file>... `
- 뒤에 파일명을 적지 않으면 stage에 올라간 파일 모두가 내려감

### git commit 되돌리기(아직 local에 있는 경우)

### 1. commit message 수정하기

#### 1.1. 가장 최근 commit 수정

```bash
git commit --amend
```

위와 같이 `amend` 를 이용하면 **가장 마지막에 commit 한 내용**을 수정할 수 있습니다.



#### 1.2. 더 오래된 commit 수정 or 한 번에 여러 commit 수정

커맨드 라인에 `git log` 를 입력하여  어떤 커밋을 수정할지 확인합니다.

만약 가장 최근 한 커밋으로부터 세 번째 커밋을 수정해야 한다면

```bash
git rebase -i HEAD~3
```

위 커맨드를 사용하면 현재 작업중인 브랜치의 가장 최근 commit 3개를 보여주게 됩니다.

(3이 들어간 자리에 체크하길 원하는 commit 의 갯수를 집어넣으시면 됩니다!)


이젠 수정하고 싶은 커밋 옆의 `pick` 이라는 문구를 `reword` 로 바꿔 주면 됩니다.

```bash
pick e499d89 Delete CNAME
reword 0c39034 Better README
reword f7fde4a Change the commit message but push the same commit.
```

`esc` -> `:wq` 를 통해 커밋 리스트를 저장을 해주고 나면, 두 개의 커밋을 각각 수정할 수 있는 창이 순서대로 띄워집니다.

원하는대로 커밋을 수정하시고, `:wq` 를 통해 저장해주세요.

수정이 잘 되었는지 `git log` 를 통해 확인합니다.



### git push 되돌리기 (협업환경에서 권장하지 않음)



## 2. 이미 push한 이름 변경

### 파일명, 폴더명 변경

1. 이름을 변경하려는 디렉토리의 상위로 이동
2. `git mv oldName newName` 입력
3. `git add` `git commit` 하면 반영



### 경로변경

````bash
git mv ./folder1/test.py. ./folder2/test.py
````



## 3. 깃허브 브랜치 그래프로 보여주기

```bash
git log --branches --graph --decorate
```



## 4. 원격 브랜치 코드 로컬 브랜치에 적용하기(tracking)

```bash
git checkout -t [원격 브랜치명]
```

다음과 같은 명령어는 원격 레포지토리의 브랜치를 로컬 브랜치에 적용하고 싶을 때, 즉 영구적으로 tracking 하고 싶을 때 `-t` 옵션을 주어서 `checkout` 



## 5. Untracked file 제거하기

- Untracked file만 제거하고 싶은 경우

```bash
git clean -f
```

- Untracked file과 디렉토리까지 제거하고 싶은 경우

```bash
git clean -fd
```





