윈도우에서 Git 설치하기
---

다운로드
---
---
<img src="/images/git_install/git_install_1.png" width="250">   

먼저 `Git`홈페이지에서 `Download for Windows`을 클릭해 자신의 윈도우 버전에 맞는 Git을 다운로드 해준다.   
    [Git 홈페이지](https://git-scm.com/)   

윈도우 버전에 맞는 `Git`이 알아서 다운로드된다.

설치
---
---
설치파일을 실행시키면  

![](/images/git_install/git_install_2.png)   
* 항상 보는 약관페이지가 나온다. `Next`를 눌러 넘어간다.   

![](/images/git_install/git_install_3.png)   
* 설치경로를 정해주고 `Next`

![](/images/git_install/git_install_4.png)   
* 설치할 Component들을 선택하는 창이다. 기본으로 선택되어 있는것만 선택하고 `Next`를 눌러 넘어간다.

![](/images/git_install/git_install_5.png)   
* 시작메뉴에 폴더를 생성하는 창이다. 폴더를 추가하고 싶지 않다면 아래에 있는 `Don't create a Start Menu folder` 체크박스를 클릭하고 `Next`를 눌러준다.

![](/images/git_install/git_install_6.png)   
* `Git`의 기본 에디터를 설정하는 창이다. 이번에도 기본으로 선택되어있는 항목을 고르고 `Next`를 눌러 넘어간다.

![](/images/git_install/git_install_7.png)   
* 선택되어있는 `Let Git decide`를 고르고 `Next`를 누른다.

![](/images/git_install/git_install_8.png)   
* 환경변수 옵션 설정이다. `Git from the Command line and also from 3rd-party software`를 선택하고 `Next`

![](/images/git_install/git_install_9.png)   
* `Use bundled OpenSSH`를 선택한채로 `Next`를 누른다.

![](/images/git_install/git_install_10.png)   
* https 전송시 인증서 선택. `Use the OpenSSL library`을 선택 후 `Next`

![](/images/git_install/git_install_11.png)   
* `Checkout Windows style, commit Unix-style line endings`을 선택하고 `Next`

![](/images/git_install/git_install_12.png)   
* `Git Bash` 터미널의 형식. `Use MinTTY`를 선택하고 넘어갑니다.

![](/images/git_install/git_install_13.png)   
* Git pull 작업방식. `Default`로 설정해주고 `Next`를 누른다.

![](/images/git_install/git_install_14.png)   
* Credential Helper 사용에 대한 선택. `Git Credential Manager Core`선택 후 `Next`

![](/images/git_install/git_install_15.png)   
![](/images/git_install/git_install_16.png)   
* 기타 실행옵션. 필자는 `Enable file system caching`만 체크 후 넘어갔다.

![](/images/git_install/git_install_17.png)   
* 모든 옵션에 체크를 완료하고 설치가 진행되는 모습.

![](/images/git_install/git_install_18.png)   
* 설치가 완료되면 위와 같은 창이 뜬다.

설치 확인
---
---
자 이제 설치가 잘 되었는지 확인할 차례이다.
윈도우에 `cmd`를 검색해 명령 프롬프트를 실행한다.
아무것도 하지않은채로 git 을 입력한다.   

![](/images/git_install/git_install_19.png)
입력하면 위 사진처럼 `Git`의 명령어가 나오면서 설치가 완료된걸 확인 할 수 있다.