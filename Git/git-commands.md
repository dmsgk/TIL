

# 자주 사용하는 Git 명령어

## 1. 되돌리기

### 원격저장소에 올려둔 상태로 프로젝트 되돌리기

- ```
  git fetch --all
  git reset --hard origin/main
  ```

- 아니면 `git checkout .`

### git add 되돌리기

- `git reset HEAD <file>... `
- 뒤에 파일명을 적지 않으면 stage에 올라간 파일 모두가 내려감

### git commit 되돌리기

### git push 되돌리기 (협업환경에서 권장하지 않음)



## 2. 이미 push한 이름 변경

### 파일명, 폴더명 변경

1. 이름을 변경하려는 디렉토리의 상위로 이동
2. `git mv oldName newName` 입력
3. `git add` `git commit` 하면 반영



### 경로변경

````
git mv ./folder1/test.py. ./folder2/test.py
````



## 3. 깃허브 브랜치 그래프로 보여주기

```
git log --branches --graph --decorate
```



## 4. 원격 브랜치 코드 로컬 브랜치에 적용하기(tracking)

```null
$ git checkout -t [원격 브랜치명]
```

다음과 같은 명령어는 원격 레포지토리의 브랜치를 로컬 브랜치에 적용하고 싶을 때, 즉 영구적으로 tracking 하고 싶을 때 `-t` 옵션을 주어서 `checkout` 



## 5. Untracked file 제거하기

- Untracked file만 제거하고 싶은 경우

```
git clean -f
```

- Untracked file과 디렉토리까지 제거하고 싶은 경우

```
git clean -fd
```





