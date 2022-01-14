---
title: 자바스크립트(Javascript) 기록-4  
date: 2022-01-13 20:48:56  
categories:   
- Javascript  

tags:  
- Javascript
- stub
---

## 태그 다루기

---

중간제목에서 말하는 태그를 다룬다는 것은 태그의 내부 속성을 수정한다는 것이다.

강의에서 나왔던 대로 h1태그를 사용하여 적어보면

```jsx
h1.className = "";
```

가장먼저 클래스를 바꿀수 있는 속성인 `.className`이다.

“” 내부에 입력한 클래스로 바뀌게 되는데 문제는 원래 있던 클래스가 사라지고 입력한 클래스만 새로 추가되는 것이다.

```jsx
h1.classList.(Element)
```

그래서 `.classList`를 불러와 클래스를 추가하는 방법이 있는데 

추가는 `h1.classList.add`로 클래스를 추가 할 수 있으며,

삭제는 `h1.classList.remove`로 삭제가 가능하다.

여기에 if문을 추가해준다면 특정 이벤트(클릭 등)에 따라 클래스의 추가와 삭제가 반복되게 만들수도 있다.

그런데 이렇게 반복을 하게 할때는 `add`와 `remove`를 쓰면 코드가 길어지게 되는데 이럴때를 위해 있는게 `toggle` 속성이다.

```jsx
if (h1.classList.contains("clicked")) { // .contains()는 괄호 내부의 클래스가 존재하는지 확인
	h1.classList.remove("clicked");
} else {
	h1.classList.add("clicked");
}
```

`add` 와 `remove` 를 쓰면 다섯줄이였던 코드가

```jsx
h1.classList.toggle("clicked");
```

`toggle`을 사용하면 이정도로 줄어들게 된다.

설명에 생략이 매우 많지만 사용법은 대략 이렇다.

이외에도 태그별로 많은 속성이 있으며, [MDN Web Docs](https://developer.mozilla.org/ko/docs/Web/API/Element) 에서 찾아볼 수 있다.

## .preventDefault

---

`.preventDefault`는 이벤트가 발생했을때 그 이벤트의 기본동작을 막는다.

예를들어 ‘submit’ 이벤트가 발생했을때 브라우저는 기본적으로 페이지를 새로고침한다.

이런것들이 기본동작인데 이를 막아주는것이 `.preventDefault` 이다.

사용 예는 다음과 같다.

```jsx
function func(event) {
	event.preventDefault();
	console.log(event);
}
```

이렇게 이벤트의 동작을 막고 콘솔에서 이벤트의 로그를 볼 수 있다.

새로고침을 막는등의 기능 이외에도 클릭시 링크로의 이동을 막거나, form의 제출을 막는등 여러가지를 할 수 있다.

## 백틱(``)으로 문자열 작성

---

문자열과 변수를 합쳐서 출력하려면 언어를 처음 배우기 시작한 사람들은 보통 다음과 같이 출력할 것이다

```jsx
const a = "world";
console.log("hello " + a;);
```

그런데 파이썬의 포맷함수처럼 사용할수 있는 기능이 JS에도 있다.

사용법은 다음과 같다.

```jsx
const a = "world";
console.log(`hello ${a}`);
```

띄어쓰기를 따로 생각하지 않아도 되고 `+` 부호가 지저분해보였기 때문에 이 방법이 필자에게는 더욱 깔끔해 보였다.