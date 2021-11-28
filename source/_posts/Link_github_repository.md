---
title: Github Repository생성 및 로컬 저장소 연결, 업로드 명령어  
date: 2021-11-26 17:11:08  
categories: 
- Github  

tags:
- Github
- Repository
- Link
---

## Github repository 생성

---


![Github repository 생성](/images/Link_github_repository/capture-1.png)  
로그인된 깃허브 홈페이지에서 Your repositories > 우상단 `New` 버튼을 클릭한 후 `Repository name`을 입력하여 리포지토리를 생성한다.  

## Repository와 로컬 저장소를 연결

---
![폴더 생성 및 터미널 실행](/images/Link_github_repository/capture-2.png)  
Repository와 같은 이름으로 폴더를 하나 생성해 준 후 폴더 아무곳이나 우클릭하여 `Git Bash Here`로 터미널을 실행해준다.
<br><br>
```commandlin
$ cd [Directory]
```
디렉토리 주소를 입력하면 바탕화면에서 터미널을 실행하여 명령어로 진입 할 수도 있다.
<br><br>
```commandline
$ git init
```
명령어를 입력해 업로드할 폴더에서 깃을 init한다.(로컬 저장소 생성)

![생성한 Repository의 주소 복사하기](/images/Link_github_repository/capture-3.png)  
우측의 copy버튼을 클릭하여 주소를 복사한다.
<br><br>
```commandline
$ git remote add origin [Repository URL]
```
명령어를 입력해준 후 위에서 복사했던 주소를 붙여넣어준다. (Git Bash에서의 붙여넣기는 Shift + Insert)

### Repository URL을 잘못입력했다면 아래 명령어들을 참고하면 된다.

- 현재 로컬 저장소의 Repository URL 확인 : `$ git remote -v`
- 현재 로컬 저장소의 Repository URL 변경 : `$ git remote set-url origin [재설정할 Repository URL]`
- 현재 로컬 저장소의 Repository URL 삭제 : `$ git remote remove origin`

## 로컬 저장소에 있는 파일을 업로드

로컬 저장소에 있는 파일을 깃허브에 업로드하기 위해서는 다음 세가지의 명령어를 차례로 입력해주어야 한다.
<br><br>
```commandline
$ git add .
$ git add file.py
```
위처럼 add 명령어로 commit 될 대상에 파일을 포함시킬수 있다.  
add . 은 변동사항이 있는 모든파일을, 두번째줄은 해당파일만 포함시킨다.  
<br><br>
```commandline
$ git commit -m "표시할 메세지"
```
파일을 커밋하고 그 커밋에 대해 간단한 메세지를 남기는 명령어이다.
<br><br>
```commandline
$ git push
$ git push origin HEAD:master
```
커밋한 파일들을 깃허브로 올려주는 명령어이다.
첫째 줄 명령어로 푸시가 안된다면 아래 명령어를 입력해보자

![로컬 저장소와 리포지토리가 잘 연결되어 커밋된 모습](/images/Link_github_repository/capture-4.png)  

성공적으로 연결되어 커밋, 푸시까지 된 모습이다.
