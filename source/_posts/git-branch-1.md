---
title: git branch 기초 (추가,이동,삭제 등)  
date: 2021-12-10 17:12:33  
categories: 
- git  

tags:
- git
- github
- branch
- version
- checkout
---

heroku를 통해서 대시보드 배포를 하려고 애를 쓰던중에 끝도없는 에러와 마주쳐서 github Repo를 지웠다 만들었다 하기를 열번가량 반복하다가 현타가 왔다.  
강사님이 주신 [URL](https://torch-law-f0b.notion.site/Heroku-Dash-Windows-10-b3a5d5e6ecea4ff5a896f18b24c080ab) 대로하면 가장 기본적인 배포는 가능하니 처음것을 백업해놓고 이것저것 고쳐가며 써보자 하는 생각이 들자 git이 애초에 그런(버전 관리) 프로그램이었다는 게 생각나 찾아보고 포스팅하게 되었다.

## 그래서 branch가 뭔데?
___
branch는 git에서 독립적으로 어떠한 작업을 진행하기 위한 개념이다.  
각각 나누어진 branch는 서로 영향을 주거나 받지 않기 때문에 여러작업을 동시에 진행해볼 수 있다.
또, 이렇게 나누어진 branch는 다른 branch와 병합하거나 덮어씀으로써 작업한 내용을 새로운 하나의 브랜치로 모을 수 있다.


![branch의 설명도](/images/git-branch/git-branch-info.png)

위의 그림처럼 branch에서 서비스추가, 버그수정 등을 하고 main branch에 병합시키는 것이다.
branch 에서 작업을 하다가 문제가 되어도 폐기하고 main branch에서 새로 branch를 만들면 되니 원본 손실의 위험도 없다.

## 그럼, 어떻게 쓰는건데?
___
branch의 명령어는 꽤나 다양하지만 이 포스팅에서는 추가,이동,삭제등의 기본적인 것만들 다루겠다.(추후 포스팅 예정)  

## branch 확인

branch를 추가, 이동, 삭제하기 전에 Repo에 어떤 branch가 있는지 확인해야한다.(동명의 branch는 만들어지지 않는다.)  
확인을 하기 위해서는 Repo의 디렉토리에서 터미널이나 git bash로 다음 코드를 작성한다.  
``` 
git branch 
```

![branch 확인](/images/git-branch/git-branch-1.png)

branch에 대해 처음 알았고 아무 조작도 가하지 않았다면 아마도 master(또는 main) branch만 있을 것이다.  
그리고 현재 적용(?)된 branch 가 색이 다르며 앞에 별표(*)가 있다.

## branch 추가

이제 새롭게 branch 를 만들어보자 만약 자신이 원하는 branch 의 이름이 bugfix 라면 터미널에 다음처럼 작성하면 된다.  
```python
# git branch "branchName"
git branch bugfix
```
별다른 반응 없이 추가가 됐을 것이다.  
확인을 위해 다시 `git branch` 를 해보면..  

![branch 추가 후 확인](/images/git-branch/git-branch-2.png)

이렇게 새로 branch가 만들어 졌을것이다.  

## branch 이동
branch를 새로이 만들었으니 이젠 새로 만든 branch에서 작업을 하기위해 이동을 해야한다.  
이동하는 명령어는 다음과 같다.  
```python
# git checkout "branchName"
git checkout bugfix
```

![branch 이동 후 확인](/images/git-branch/git-branch-3.png)

branch를 이동했으며 bugfix 가 활성화 된 것이 보인다.

## branch 삭제

필요없는 branch를 어떻게 삭제 할까?  
```python
# git branch -d "branchName"
git branch -d bugfix
```

![branch 이동 및 삭제 후 확인](/images/git-branch/git-branch-4.png)

현재 활성화된 branch를 삭제하려는 경우에는 삭제되지않으니 `checkout`으로 다른 branch로 이동한 다음 삭제를 시켜줘야 한다.

이렇게 branch 의 기본적인 명령어들을 알아보았는데 클론을 만들고 클론이 잘못될 경우 다시 되돌릴수 있다는 것 자체가 매우 필요한 기능이라 자주 사용하게 될듯 하다.  

