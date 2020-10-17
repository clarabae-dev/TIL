## Git  
리누스 토발즈가 개발한 분산형 버전 관리 시스템.  
  
  
  
### 기본 개념  
1. 초기화  
트래킹하고자 하는 폴더로 이동해 초기화 명령어부터 시작한다.  

```cli
git init
```  
  
.git 이라는 숨김 폴더가 생성되는데, 이를 저장소라 부른다. git은 폴더의 모든 변경 내용을 이 저장소에 저장한다.  

2. 스테이징  
git이 파일의 변경 내역을 저장할 때, 곧바로 저장하는 것이 아니라 스테이징이라는 단계를 거친다.  
스테이징은 변경사항 중 *저장하고 싶은 부분만 선택하여 임시로 저장*하는 개념이다.  
  
```cli
git add file.swift
```  
  
add 명령어를 통해 추적하고 싶은 파일을 스테이지에 넣을 수 있다. 스테이징 된 파일은 커밋 직전 상태로 변경된다.  

3. 커밋  
git이 변경 내용을 저장하는 단위를 커밋 이라 한다. 먼저 스테이지 상태에 두어야 비로소 커밋을 만들 수 있다.  
  
```cli
git commit
```  
  
스테이지에 있는 내용을 커밋으로 만들기 위해 위의 명령어를 사용하면, 기본 에디터가 열리고 변경 내용에 대한 설명을 기록할 수 있는 입력 화면이 나온다.  
  
```cli
git commit -m "커밋 메세지"
```  
  
에디터 없이도 -m 옵션을 활용해 바로 메세지를 입력할 수 있다.  
  
```cli
git commit -am "스테이지하고 커밋함"
```  
  
옵션 -a는 신규 파일을 제외한 트래킹하는 모든 파일의 변경사항을 스테이징하고 커밋하는 옵션이다.  
  
```cli
git commit --amend
```  
  
옵션 --amend는 커밋을 신규 생성하지 않고 이전 커밋에 추가하고자 할 때 사용하는 옵션이다. 에디터에서 이전 커밋 메세지를 수정할 수 있다.  

4. 로그  
  
```cli
git log

commit 7446c9a3569deaf38915b3bd456cb256f06ee67b
Author: clarabae-dev <clarabae.dev@gmail.com>
Date:   Thu Oct 8 18:06:52 2020 +0900

    readme 수정
```  
  
커밋 내역들을 확인할 수 있는 명령어 이다. 커밋 식별자인 해쉬값, 커밋 작성자, 작성일자, 커밋 메세지를 확인할 수 있다.  
  
```cli
git show

-DispatchQueue 대신 RxSwift 변경
+- DispatchQueue 대신 RxSwift 변경
+- Unit Test 추가
```  
  
show는 변경 내용을 확인할 수 있는 명령어이다. 삭제된 라인은 -, 추가한 라인은 +로 표시한다.  
  
```cli
git show 7446c9a3569deaf38915b3bd456cb256f06ee67b
```  
  
특정 커밋의 변경 사항은 로그의 커밋 해쉬값으로 확인할 수 있다.  

5. 브랜치  
다른 종류의 작업을 수행하고자 할 때 브랜치를 만든다. git은 master 브랜치를 기본으로 가지고 있다.  
  
```cli
git branch

* master
```  
  
git branch 명령어로 생성되어 있는 브랜치 목록을 확인할 수 있다.  
  
```cli
git branch signup master
```  
  
신규 브랜치를 추가하고자 할 때 사용하는 명령어이다. git branch '생성할 브랜치명' '생성한 브랜치가 추가될 기준 브랜치명'  
  
```cli
git checkout signup
git branch

* signup
  master
```  
  
브랜치를 변경하려고 다른 브랜치를 선택하는 것을 *체크아웃한다* 라고 표현한다. 브랜치 목록에서 사용 중인 브랜치 앞에는 * 가 붙는다.  
  
```cli
git checkout -b signup
```  
  
옵션 -b는 브랜치를 만들고 해당 브랜치로 체크아웃하는 옵션이다.  
  
```cli
git checkout master
git merge signup
```  
  
signup 브랜치를 master 브랜치에 병합하기 위해 기준점인 master 브랜치로 체크아웃한 후 merge 명령어를 사용한다.  

6. 헤드  
자신의 현재 위치를 더 자세하게 담고있는 정보를 헤드라 부른다.  
  
```cli
git log

commit 06fb0e48f7a87fb34f128a121294f6f475e511ad (HEAD -> master, origin/master)
```  
  
master 브랜치에 헤드 표시가 되어있으므로 현재 작업하고 있는 위치라는 뜻이다. 브랜치 내부 특정 커밋으로 체크아웃할 때도 헤드가 이동한다.  
  
### Git-flow  
1. 종류  
- master: 출시될 수 있는 브랜치이며 가장 마지막으로 merge되어야 하는 브랜치이다. 출시된 master 브랜치에는 버전 태그를 추가한다.  
- develop: master에서 시작하여 다음 출시 버전을 개발하는 브랜치이다. 상시로 버그를 수정한 커밋들이 추가된다.  
- feature: 항상 develop에서 시작하여 기능을 개발하는 브랜치이다. 작업이 완료되면 feature는 develop에 merge된다.  
- release: 이번 출시 버전을 준비하는 QA용 브랜치이다. develop에 이번 버전에 포함되는 모든 기능이 merge되면 QA를 위해 develop에서부터 release를 생성한다.  
		   QA를 진행하면서 발생하는 버그들은 release에 수정된다. QA 종료 후, release를 master와 develop에 각각 merge 한다.
- hotfix: 출시 버전에서 발생한 버그를 수정하는 브랜치.  
  
![Alt text](https://woowabros.github.io/img/2017-10-30/git-flow_overall_graph.png)  
  
  
### Pros and Cons  
1. Pros  
- 오프라인 작업이 가능하다. git은 원격 저장소를 로컬에 복제하고, 로컬 저장소에 있는 히스토리도 유지된다.  
서버에서 새 자료를 받아올 수 없을 뿐, 오프라인 상태에서도 대부분의 형상 관리 기능을 사용할 수 있다.  
- 일시적 서버 장애가 발생하더라도 개발을 계속할 수 있다.  
- 중간 서버, 부서별 서버 등 분산처리 구조를 유연하게 세울 수 있다.  
- branch, 가지치기가 비교적 가볍다. branch는 대부분의 형상 관리 도구가 지원하는 기능이다.  
다만, git은 branch를 만드는 것이 쉽고 가벼워 원하는 만큼 별다른 제약없이 생성하고 삭제할 수 있다.  
- 병합에서 발생하는 문제가 적다. 서버의 자료를 가져와 로컬에서 병합한 뒤 이를 다시 올리는 형태이기 때문이다.  
- 스테이징을 지원한다. 커밋하기 전 사용할 수 있는 staging 단계가 따로 존재한다.  
2. Cons  
- 덜 직관적이고 배우기 어렵다. commit, push, pull merge, fetch 등 수많은 용어가 존재.  
- 한번에 여러 브랜치나 여러 태그에 걸쳐 커밋할 수 없다. 내가 작성한 변동사항이 다른 브랜치에 자동으로 반영되지 않고, 취합할 때 반영된다.  
- 하나의 저장소가 하나의 프로젝트 전체를 의미하는 것으로 되어 있어 일부만 클론하는 등을 할 수 없다.  
- push를 하였어도 히스토리가 영구적으로 안전하게 저장된다고 보장할 수 없다. 해당 브랜치가 다른 브랜치에 병합되기 전 삭제되면 추후 해당 브랜치에 접근할 수 없다.  
  
  
  
출처:  
https://namu.wiki/w/Git  
https://jeonghwan-kim.github.io/dev/2020/02/10/git-usage.html  