---
title: 마크다운(Markdown) 문법
date: 2021-11-04 16:55:59
categories: 
- Markdown
tags:
- Markdown
- Grammar
---
지금 당장만 해도 이 글을 마크다운으로 작성하고 있는 나는 HTML를 접해보긴 했지만 자유자재로 쓸 수 있는정도는 아니였기에 깃허브 블로그를 시작하면서 마크다운의 문법에 대해 알아야 할 필요가 생겼다.  


다른 포스트들도 마찬가지지만 더욱 이 포스트는 자주 찾아 봐야 할 것 같기에 문법만을 기록하며, 접기를 최대한 지양한다.

## 마크다운 문법

---
### 제목 작성
```markdown
# 이러면 큰제목 <h1>태그
## 이러면 중간제목 <h2>태그
### 이러면 작은제목 <h3>태그
#### 도 되긴 하지만 굵게한 글자와 차이가 없음. <h4>태그로 사용된다
```
# 이러면 큰제목 `<h1>`태그
## 이러면 중간제목 `<h2>`태그
### 이러면 작은제목 `<h3>`태그
#### 도 되긴 하지만 굵게한 글자와 차이가 없는 `<h4>`태그로 사용된다

---

### 줄바꿈

```markdown
줄바꿈은 행의 끝에서 공백 두칸을 주고  
다음행에 작성하면 된다
```
줄바꿈은 행의 끝에서 공백 두칸을 주고  
다음행에 작성하면 된다

---

### 코드블럭

```markdown
```과 ~~~는 마크다운의 내용을 코드블럭을 씌운다.
```(언어명) 내용 ``` 의 형태로 작성하며
이것도 코드블럭으로 씌워진 것이다.
```
### 인라인코드
```markdown
이것은 `인라인코드`이다.
```
이것은 `인라인코드`이다.

---

### 링크 걸기

www.naver.com  
그냥 주소를 써도 링크로 클릭이 되지만 
```markdown
[WJ 블로그](cincu4221.github.io)
```
[WJ 블로그](cincu4221.github.io)  
위처럼 작성하면 주소를 숨기고 텍스트에 링크를 걸 수 있다.

---

### 텍스트

```markdown
**강조된 텍스트**
```
**강조된 텍스트**
<br><br>
```markdown
*기울인텍스트*
***기울임,강조를적용한텍스트***
```
*기울인텍스트*  
***기울임,강조를적용한텍스트***
<br><br>
```markdown
~~취소선입니다~~
```
~~취소선입니다~~

<br><br>

글자색
```markdown
<span style="color:orange">주황색 글씨</span>  
<span style="color:yellow">노란색 글씨</span>  
<span style="color:#FF0000">빨간색 글씨</span>  
<span style="color:blue">파란색 글씨</span>  
<span style="color:green">초록색 글씨</span>  
<span style="color:pink">분홍색 글씨</span> 

<span style="color:#00FFFF">헥스코드 적용 글씨</span>
```
<span style="color:orange">주황색 글씨</span>  
<span style="color:yellow">노란색 글씨</span>  
<span style="color:#FF0000">빨간색 글씨</span>  
<span style="color:blue">파란색 글씨</span>  
<span style="color:green">초록색 글씨</span>  
<span style="color:pink">분홍색 글씨</span> 

<span style="color:#00FFFF">헥스코드 적용 글씨</span>

검색하기 애매한 색도 [여기](https://www.color-hex.com/) 에서 찾을 수 있다.



---

### 구분선

```markdown
***
-- --
---
```
***
-- --
---

<br><br><br>

---

## 표만들기
```markdown
|제목|제목|
|:---:|:---:|
|내용|내용|
|||
```

|제목|제목|
|:---:|:---:|
|내용|내용|
|내용|내용|

앞으로 계속 추가