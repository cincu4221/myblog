---
title: Heroku로 HTML 페이지 배포하기  
date: 2022-01-07 17:23:00  
categories:   
- deploy 

tags:
- heroku
- deploy
- stub

---

캐글 대시보드 배포 프로젝트를 마치고 꽤나 지났을때, 학원에 다니기 한참 전에 HTML과 CSS 로만 만들었던 카카오톡 클론코딩 프로젝트가 생각나 그것도 배포하는 김에 쓰는 글.

## 사전준비

---
- Heroku 계정
- Heroku CLI
- Git

일단 Heroku에서 배포를 할 것이므로 [Heroku](https://www.heroku.com/) 의 계정과 [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) 설치가 필요하다.  
[Git](https://git-scm.com/) 도 자신의 환경에 맞추어 설치해주자. [윈도우에서 Git 설치하기](https://cincu4221.github.io/2021/10/29/setting_Git/)

node.js가 설치되어 있는 경우에는 npm 으로 간편히 설치가 가능하다고 한다.
```
npm i -g heroku
```

설치가 잘 됐나 확인해보자
```
heroku -v
```
버전이 출력되면 잘 설치가 된 것이다.
```
heroku login
```
설치가 잘 완료되었으면 heroku login을 입력하자.  
그러면 브라우저 창이 하나 뜨고, heroku계정을 입력하면 준비 완료.
<br><br><br>

## HTML 파일을 Heroku로 배포하기

---

프로젝트를 로컬에서 완성했다고 바로 heroku로 배포하면 heroku가 어떤 언어로 개발한 프로젝트인지 모르기 때문에 다음과 같은 오류를 내며 구동되지 않는다.  
![짚히는곳 없으면 개고생 시작](/images/heroku-deploy-html/deploy_fail.png)  
코린이 입장에서 프로젝트 만들었다고 싱글벙글하다가 에러나면 진짜 아찔하다.  
그래서 이런일이 없게 heroku에서 지원하는 언어들중 하나인 php 프로젝트로 인식되게 처리해 주어야 한다.  
프로젝트의 루트 디렉토리에 다음처럼 html 파일로 리다이렉트 시켜주는 php 파일만 하나 만들어주면 된다.
### index.php
```
<?
    header('Location: /index.html');
?>
```

이제 파일은 모두 완료됐으니 CLI를 이용해서 heroku에 배포를 해보자.  
당연히 아래의 명령을 입력하는 위치는 프로젝트의 루트 디렉토리여야 한다.  
```
# 저장소를 만들고 커밋 (github연결과는 무관)
git init
git add .
git commit -m "first commit"

# 새로운 Heroku app 생성
heroku create

# Heroku에 push하기
git push heroku master
```
이렇게 하면 배포는 마무리 됐다.  

이외에도 같이 필요할것같은 몇가지 명령어를 적어보자면
<br><br><br>

### 파일 수정 후 재배포시
```
git add .
git commit -m "커밋 메모"

git push heroku master
```

### Heroku app 이름 바꾸기
heroku create로 app을 만들면 이름이 임의로 생성된다 그렇기때문에 이름을 바꾸고 싶다면 아래의 명령어를 사용하면 된다.  
```
heroku apps:rename <새 이름> --app <기존 이름>
```

### heroku app 열기
heroku app 페이지에서 open app 버튼을 통해 여는 방법도 있으나 CLI를 통해 바로 열어보고 싶다면 다음 명령어를 사용하자.
```
heroku open
```

### heroku git 과 git 저장소 연결 명령어
본 포스팅에서는 폴더에서 app을 만들었기때문에 바로 연결되어 사용할 필요가 없었던 명령어이다.  
그러나 저장소의 주소가 필요하거나 변경할 경우를 위해 기록한다.
```
git remote -v # 폴더와 연결된 저장소(heroku git, github 등)의 주소가 출력됨
git remote set-url heroku <변경할 git 경로> # heroku저장소의 주소를 변경할 경우 사용, 변경할 git 경로의 예)https://git.heroku.com/<app이름>.git
```

### 오류발생시 로그 출력
배포를 진행하다 보면 오류가 발생할 수 있다.  
그럴 경우 로그를 출력하여 에러코드를 확인하고 **영어로** 구글링하여 답을 찾도록 하자.
```
heroku logs
heroku logs --tail
```


<br><br><br>

# Reference.

- [heroku에 일반 html 사이트 올리기](https://stove99.github.io/etc/2019/08/08/static-web-site-deploy-to-heroku/)
- [[Hosting] heroku.com 사용하기](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=chrisphotography&logNo=221177828341)