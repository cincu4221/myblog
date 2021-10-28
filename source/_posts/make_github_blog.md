---
Hexo로 깃허브 블로그 만들기
---

## Hexo란?
    Hexo는 Node.js기반의 정적 블로그 프레임워크 입니다.   
**Markdown**으로 문서를 작성하고 빌드시 정적 HTML이 생기고   
이것을 GitHub pages에 배포 하여 블로그를 관리 합니다.

## 설치환경
* Git
* Node.js
* 파이참(PyCharm)
* GitHub 계정
<!--설치법은 따로 포스팅하고 링크할것--><br>
## 설치환경 확인
1. 아래 코드로 Node.js 설치를 확인해봅니다.
```
$ node -v
```
2. 아래 코드로 Git 설치를 확인합니다.
```
$ git --version
```
3. npm을 통해 hexo를 전역으로 설치합니다.
```
$ npm install -g hexo-cli
```
## GitHub 블로그 만들기
먼저 원하는 디렉토리로 이동하여 헥소 블로그 디렉토리를 만들어줍니다.(이 포스팅에서는 myblog)
```
$ hexo init myblog
```
생성된 디렉토리를 우클릭 한 뒤   
'**Open Folder as PyCharm Community Edition Project**'를 클릭해 파이참으로 열어줍니다.
![myblog_pycharm.png](source/img/myblog_pycharm.png)

실행된 파이참의 좌측 아래에서 터미널 메뉴를 선택하고 사진과같이 Git Bash를 클릭해주면   
파이참에서 Git을 사용할 수 있게 됩니다.
![pycharm_terminal.png](source/img/pycharm_terminal.png)   

이후 Git에서 다음 명령어들을 입력해줍니다
```
$ npm install
$ npm install hexo-server --save
$ npm install hexo-deployer-git --save
```

이제 GitHub 접속하고 우측 상단의 아이콘 클릭 후 '**Your repositories**'에 들어갑니다.
![github_create_new_repositories.png](/source/img/github_create_new_repositories.png)
Repository name 란에 만들었던 디렉토리와 같은 이름인 'myblog'를 넣은 후 아무것도 건드리지 않고 아래의 'Create repository' 버튼을 눌러줍니다.   

다시 파이참으로 돌아와서 아래의 Git 명령어들을 입력해줍니다.
```
echo "# myblog" >> README.md
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/cincu4221/myblog.git
git push -u origin main
```

GitHub에서 'myblog' 리포지토리를 만들때와 이름만 다르게 '사용자계정명.github.it' 으로 바꾸어서 리포지토리를 하나 더 생성해 줍니다.

파이참의 작업영역에서 _config.yml 파일을 열어서 수정해줍니다.
###블로그 정보 설정
```yaml
title: blog title
subtitle: 부제목을 지어주세요
description: description을 지어주세요
author: YourName
```
###블로그의 URL정보 설정
```yaml
url: https://Username.github.io
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```
###깃허브 연동 설정
```yaml
# Deployment
deploy:
  type: git
  repo: https://github.com/Username/Username.github.io.git
  branch: main
```
* 위의 코드에서 Username으로 되어있는것은 꼭 사용자의 GitHub계정명으로 바꿔주셔야 합니다.

파이참의 Git Bash(Terminal)에 다음 코드들을 입력합니다.
```
$ hexo generate
$ hexo server
```
이후 나오는 [localhost:4000](http://localhost:4000)에서 화면이 뜨는지 확인합니다.
   
다음 코드를 입력해 최종적으로 배포를 진행합니다.
```
$ hexo deploy
```
배포가 완료되면 브라우저에서 [USERNAME.github.io]로 접속해 정상적으로 배포되었는지 확인합니다.