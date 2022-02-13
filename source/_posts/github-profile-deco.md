---
title: 깃허브 프로필 꾸미기
date: 2022-02-12 14:53:39  
categories:   
- Github 

tags:
- Github
- profile
---


아직까지 꾸준히 깃허브와 블로그를 통해 글을 쓰고있지만 사실 처음부터 마음에 걸렸던 것이 두 가지가 있다.

그건 블로그의 테마(현재 ICARUS)와 다른사람들에 비해 아무 손질도 안한듯한 내 깃허브 프로필인데 이 두 가지 중 오늘은 깃허브 프로필을 조금이라도 꾸며보려고 구글링을 하고 포스팅도 한다.

일단 지금 포스팅과 꾸미기를 동시에 할 예정인데 아래는 꾸미기 전의 내 프로필이다.

![Untitled](/images/github-profile-deco/Untitled.png)

뭔가 있긴 있어도 재미없고 딱딱한느낌이다

## 리포지토리 생성

---

![Untitled](/images/github-profile-deco/Untitled%201.png)

깃허브에는 숨겨진 기능이 있는데, 바로 자신의 닉네임으로 리포지토리를 만드는 것이다.

이 리포지토리는 깃허브 프로필에 README.md를 추가해 주는데 이를 통해서 프로필을 꾸밀수 있다.

이후 리포지토리 연결은 [여기](https://cincu4221.github.io/2021/11/26/Link_github_repository/)를 참고하면 된다.

![Untitled](/images/github-profile-deco/Untitled%202.png)

만약 README.md가 추가되지않았다면 간단히 추가할 수 있다. (이후 git pull을 통해 로컬로 당겨와 동기화 필수)

![Untitled](/images/github-profile-deco/Untitled%203.png)

기본적으로 만들어진 README.md의 프로필 적용모습

![Untitled](/images/github-profile-deco/Untitled%204.png)

파일에는 주석으로 간단한 설명들이 적혀져 있고, 이젠 이 README.md를 꾸며주면 된다.

## [Shields.io](http://Shields.io) 를 통해 README에 뱃지넣기

---

![Untitled](/images/github-profile-deco/Untitled%205.png)

다른사람들의 깃허브 프로필을 보면 위와같은 뱃지들이 있는것을 자주 볼수 있다.

이뻐보이는데? 나도 안 할 수 없다 프로필에 뱃지를 넣는 방법을 알아보자

1. README.md에 다음과 같이 코드를 작성한다.

```markdown
<a href="클릭시 이동할 링크" target="_blank"><img src="https://img.shields.io/badge/뱃지내용-배경색?style=뱃지모양&logo=로고이름&logoColor=로고색상"/></a>
<!--단락 상단 뱃지 코드--><a href="링크" target="_blank"><img src="https://img.shields.io/badge/GithubBlog-skyblue?style=flat&logo=Blogger&logoColor=FFFFFF"/></a>
```

각각의 설명은 다음과 같다.

- **뱃지내용**  :  뱃지에 작성될 텍스트
- **배경색** : 뱃지의 배경색

![Untitled](/images/github-profile-deco/Untitled%206.png)

등등 헥스코드사용도 가능

- **뱃지모양**

![Untitled](/images/github-profile-deco/Untitled%207.png)

위 사진 스타일 다섯가지 중 선택할수 있고 위에 단락 상단 예시의 경우엔 `flat` 을 사용했다.

사진을 보고 헷갈려서  `logo=appveyor` 까지 넣으면 안된다.

- **로고이름**

[Simple Icons](https://simpleicons.org/)

위 사이트에서 찾고싶은 아이콘을 검색하고 

![Untitled](/images/github-profile-deco/Untitled%208.png)

적당한 아이콘을 찾아 아이콘의 이름을 입력해주면 된다.(사진에선 Blogger)

- **로고색상**

로고색상은 아이콘마다 색이 있긴하지만 다른색으로 바꾸어 적용할수도 있다.

색상의 적용에 대해서는 배경색 부분 참고.

더 상세한 기능은 [Shields.io](http://Shields.io) 사이트에서 확인 후 적용 가능하다.

## README에 깃허브 스탯 표시하기

---

![Untitled](/images/github-profile-deco/Untitled%209.png)

위 뱃지들이 익숙하다면 아마 이것도 접해보지 않았을까 싶다.

바로 깃허브 스탯이다.

깃허브의 여러 정보를 알려주는 위젯? 같은건데 이걸 한번 설정해보자.

1. README.md에 다음 코드를 작성한다.

```markdown
![WooJeong's GitHub stats](https://github-readme-stats.vercel.app/api?username=유저네임&show_icons=true&theme=radical)
```

1. **유저네임** 부분을 지우고 본인 깃허브 ID를 작성한다.

 

이렇게 감사하게도 단 두단계로 이루어져있다...

테마나 아이콘을 바꿔가며 꾸밀수도 있는데 아래 링크에서 확인 할 수 있다.

[github-readme-stats/README.md at master · anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats/blob/master/themes/README.md)

## REFERENCE.

[깃허브  프로필 꾸미기!](https://80000coding.oopy.io/865f4b2a-5198-49e8-a173-0f893a4fed45)