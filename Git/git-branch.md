# Git branch 이해하기

## Master branch

배포 이력을 관리하기 위해 사용하는 브랜치. 배포 가능한 상태만을 관리함

## Develop branch

다음 출시 버전을 개발하는 브랜치. 기능개발을 위한 브랜치를 병합하여 사용.

## Feature branch

기능개발브랜치. 새로운 기능 구현하고자 할 때 develop 브랜치에서 분기해 해당 기능을 구현 후 develop 브랜치에 병합한다. 더 이상 필요하지 않은 feature branch는 삭제한다. 

```
// feature 브랜치(feature/login)를 'develop' 브랜치에서 분기
$ git checkout -b feature/login develop

/* ~ 새로운 기능에 대한 작업 수행 ~ */

/* feature 브랜치에서 모든 작업이 끝나면 */
// 'develop' 브랜치로 이동한다.
$ git checkout develop
// 'develop' 브랜치에 feature/login 브랜치 내용을 병합(merge)한다.
# --no-ff 옵션: 아래에 추가 설명
$ git merge --no-ff feature/login
// -d 옵션: feature/login에 해당하는 브랜치를 삭제한다.
$ git branch -d feature/login
// 'develop' 브랜치를 원격 중앙 저장소에 올린다.
$ git push origin develop
https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html
```

- -no-ff 옵션
  새로운 커밋 객체를 만들어 ‘develop’ 브랜치에 merge 한다.
  이것은 ‘feature’ 브랜치에 존재하는 커밋 이력을 모두 합쳐서 하나의 새로운 커밋 객체를 만들어 ‘develop’ 브랜치로 병합(merge)하는 것이다.

- ![img](https://gmlwjd9405.github.io/images/types-of-git-branch/feature-branch-merge.png)

  

- feature 브랜치 이름 정하기
  master, develop, release-(RB_), or hotfix- 제외
  [feature/기능요약] 형식을 추천 EX) feature/login
  https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html

## Release branch

이번 출시 버전을 준비하는 브랜치. 배포를 위한 전용 브랜치를 사용함으로써 한 팀이 해당 배포를 준비하는 동안 다른 팀은 다음 배포를 위한 기능 개발을 계속할 수 있다. 

‘develop’ 브랜치에서 배포할 수 있는 수준의 기능이 모이면 또는 정해진 배포 일정이 되면, release 브랜치를 분기한다.
release 브랜치를 만드는 순간부터 배포 사이클이 시작된다.
release 브랜치에서는 배포를 위한 최종적인 버그 수정, 문서 추가 등 릴리스와 직접적으로 관련된 작업을 수행한다.
직접적으로 관련된 작업들을 제외하고는 release 브랜치에 새로운 기능을 추가로 병합(merge)하지 않는다.
‘release’ 브랜치에서 배포 가능한 상태가 되면(배포 준비가 완료되면),
배포 가능한 상태: 새로운 기능을 포함한 상태로 모든 기능이 정상적으로 동작 하는 상태
‘master’ 브랜치에 병합한다. (이때, 병합한 커밋에 Release 버전 태그를 부여!)
배포를 준비하는 동안 release 브랜치가 변경되었을 수 있으므로 배포 완료 후 ‘develop’ 브랜치에도 병합한다.
이때, 다음 번 배포(Release)를 위한 개발 작업은 ‘develop’ 브랜치에서 계속 진행해 나간다.

release 브랜치 이름 정하기
release-RB_* 또는 release-* 또는 release/* 처럼 이름 짓는 것이 일반적인 관례
[release-* ] 형식을 추천 EX) release-1.2

release 브랜치 생성 및 종료 과정

```
// release 브랜치(release-1.2)를 'develop' 브랜치('master' 브랜치에서 따는 것이 아니다!)에서 분기
$ git checkout -b release-1.2 develop

/* ~ 배포 사이클이 시작 ~ */

/* release 브랜치에서 배포 가능한 상태가 되면 */
// 'master' 브랜치로 이동한다.
$ git checkout master
// 'master' 브랜치에 release-1.2 브랜치 내용을 병합(merge)한다.
$ git merge --no-ff release-1.2
// 병합한 커밋에 Release 버전 태그를 부여한다.
$ git tag -a 1.2

/* 'release' 브랜치의 변경 사항을 'develop' 브랜치에도 적용 */
// 'develop' 브랜치로 이동한다.
$ git checkout develop
// 'develop' 브랜치에 release-1.2 브랜치 내용을 병합(merge)한다.
$ git merge --no-ff release-1.2
// -d 옵션: release-1.2에 해당하는 브랜치를 삭제한다.
$ git branch -d release-1.2
```


https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html





## Hotfix branch

출시 버전에서 발생한 버그를 수정 하는 브랜치
배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우, ‘master’ 브랜치에서 분기하는 브랜치이다. ‘develop’ 브랜치에서 문제가 되는 부분을 수정하여 배포 가능한 버전을 만들기에는 시간도 많이 소요되고 안정성을 보장하기도 어려우므로 바로 배포가 가능한 ‘master’ 브랜치에서 직접 브랜치를 만들어 필요한 부분만을 수정한 후 다시 ‘master’브랜치에 병합하여 이를 배포해야 하는 것이다.

배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우,
‘master’ 브랜치에서 hotfix 브랜치를 분기한다. (‘hotfix’ 브랜치만 master에서 바로 딸 수 있다.)
문제가 되는 부분만을 빠르게 수정한다.
다시 ‘master’ 브랜치에 병합(merge)하여 이를 안정적으로 다시 배포한다.
새로운 버전 이름으로 태그를 매긴다.
hotfix 브랜치에서의 변경 사항은 ‘develop’ 브랜치에도 병합(merge)한다.



버그 수정만을 위한 ‘hotfix’ 브랜치를 따로 만들었기 때문에, 다음 배포를 위해 개발하던 작업 내용에 전혀 영향을 주지 않는다. ‘hotfix’ 브랜치는 master 브랜치를 부모로 하는 임시 브랜치라고 생각하면 된다.

hotfix 브랜치 이름 정하기
[hotfix-* ] 형식을 추천 EX) hotfix-1.2.1
hotfix 브랜치 생성 및 종료 과정

```
// release 브랜치(hotfix-1.2.1)를 'master' 브랜치(유일!)에서 분기
$ git checkout -b hotfix-1.2.1 master

/* ~ 문제가 되는 부분만을 빠르게 수정 ~ */

/* 필요한 부분을 수정한 후 */
// 'master' 브랜치로 이동한다.
$ git checkout master
// 'master' 브랜치에 hotfix-1.2.1 브랜치 내용을 병합(merge)한다.
$ git merge --no-ff hotfix-1.2.1
// 병합한 커밋에 새로운 버전 이름으로 태그를 부여한다.
$ git tag -a 1.2.1

/* 'hotfix' 브랜치의 변경 사항을 'develop' 브랜치에도 적용 */
// 'develop' 브랜치로 이동한다.
$ git checkout develop
// 'develop' 브랜치에 hotfix-1.2.1 브랜치 내용을 병합(merge)한다.
$ git merge --no-ff hotfix-1.2.1
https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html
```





![img](https://gmlwjd9405.github.io/images/types-of-git-branch/hotfix-branch.svg)

## References

- https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html