# GIT 사용법

## GIT 시작하기

git은 일종의 버전 관리 시스템(vcs)이다. 리눅스 토르발즈에 의해 만들어 졌으며, 깃허브와 깃랩 등 여러 서비스를 통해 호스팅할 수 있다.

> git init : 디렉터리 내의 파일들을 깃이라는 vcs로 관리하는 명령어 .git 폴더는 숨김 파일에 해당

## GIT의 흐름

1. **Working Directory**
   로컬 컴퓨터 환경에서 작업하는 폴더들이 위치함. 실 작업 공간이라고 생각하면 됨.<br/>
   working directory에서 staging area로 넘기려면 `git add . / {폴더명}` 을 터미널에 입력.
2. **Staging Area**
   프로젝트가 진행 중인 디렉터리 내의 모든 파일들에서의 변화가 하나 하나 세세한 버전의 차이까지 이어질 필요는 없다. 따라서 working directory에서 버전으로 묶을 것들을 staging area로 내릴 수 있음.<br/>
   staging area에서 working directory로 다시 내리기 위해서는 `git rm --cached {파일명}` 명령어를 터미널에 입력하면 됨
3. **Repository**
   staging area에 있는 파일들의 집합을 새로운 버전으로 기록하고 싶다면 `git commit -m " 커밋 메시지명"` 방식을 통해서 새로운 버전, 즉 커밋으로 만들어줄 수 있다. 앞에서의 git add .과 커밋을 동시에 진행할 수 있는 명령어는 `git commit -am "커밋 메시지명"` 이다.</br>
   Repository에는 로컬과 원격(remote)가 존재한다. 로컬은 사용자의 컴퓨터를, 원격은 깃허브와 깃랩에서의 레포지토리를 의미한다.

## GIT을 되돌리기 => reset

1. 강하게 되돌리기<br>
   working directory, staging area, repository에 있는 내역을 모두 날려버림 => `git reset --hard HEAD^`
2. 적당히 되돌리기<br>
   그냥 git reset 명령어만을 사용한다면 디폴트로 적용되는 옵션이다. Repository, staging area에 있는 것을 모두 되돌린다 => `git reset --mixed HEAD^`
3. 살짝만 되돌리기<br>
   repository에 있는 것만 날려버림 => `git reset soft HEAD^`

## GIT에서 여러 갈래를 만들기(Branch)

git을 사용하다보면 현재 나만의 흐름을 만들어 작업하고 싶은 경우가 생긴다. 이는 팀으로 협업을 할 때 각자가 맡은 역할에 집중하고 싶은 경우가 그 예시가 될 수 있다. 추후에 merge를 통해 브랜치 간의 합병도 구현할 수 있다.

1. 브랜치 만들기 : `git branch {브랜치명}`
2. 브랜치 이동 : `git checkout {브랜치명}` 추가 : `git checkout -b "{브랜치명}"` 명령어를 통해 브랜치를 새로 만들고 바로 이동할 수 있음
3. 브랜치 간의 합병 : `git merge {브랜치명}` => 현재 위치한 브랜치로 대상 브랜치를 합치기

## Reset과 Revert의 차이

> reset 명령어는 과거의 기록을 싹 날려버린다.
> revert 명령어는 과거의 기록을 **싹 날려버리는 것이 아닌,** 과거의 commit을 새로 생성하는 느낌

## 원격 저장소(remote)와의 상호작용

1. 원격 저장소의 등록 : `git remote add {원격저장소 별명} {원격 저장소 url}`
2. 원격 저장소 조회 : `git remote -v` 명령어를 통해 원격 저장소의 별명과 url을 함께 조회 가능
3. 원격 저장소의 내용을 로컬 저장소(repository)에 합쳐서 동기화 : `git pull`
4. 원격 저장소의 내용을 일단 가져오기 : `git fetch {원격저장소명}`
5. 원격 저장소에서 가져온 내용을 현재 브랜치에 합병 : `git merge {origin/main}` => origin이라는 별칭의 원격 저장소의 main 브랜치를 현재 위치한 브랜치에 합병

## 다른 사람의 프로젝트를 fork해서 기여하기(pull request)

Github를 사용하면 여러 사람들의 프로젝트를 복제하여 기여하고, merge 받는 케이스가 상당히 많다는 것을 알 수 있다. 이의 프로세스는 다음과 같다.

1. 타인의 레포지토리를 fork하여 자신의 계정에 복제된 레포지토리로 만든다.
2. 복제된 자신의 레포지토리를 `git clone {복제된 레포지토리의 url주소}` 하여 컴퓨터의 로컬 레포지토리로 가져온다.
3. 기여하고 싶은 작업을 로컬 환경에서 진행하고 복제된 원격 레포지토리로 `git push origin main` 명령어를 통해 밀어넣는다.
4. github의 원격 레포지토리에서 pull request를 날린다.
5. 원작자가 PR을 흝어보고 merge를 승인해주면 완료!<br>
   => 원작자 입장에서 pull을 해달라고 요청하는 것이므로 pull request가 아닐까?

# GIT 메시지 컨벤션
