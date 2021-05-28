

# 자주 사용하는 Git 명령어

## 되돌리기

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



### Git 이미 push한 파일명, 폴더명 변경

1. 이름을 변경하려는 디렉토리의 상위로 이동
2. `git mv oldName newName` 입력
3. `git add` `git commit` 하면 반영



### 경로변경

````
git mv ./folder1/test.py. ./folder2/test.py
````
