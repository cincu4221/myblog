---
title: 자바스크립트(Javascript) 기록-3
date: 2022-01-12 20:19:24   
categories:   
- Javascript  

tags:  
- Javascript
- stub
---

## document

---

자바스크립트는 기본적으로 HTML의 모든 항목을 읽고 변경이 가능하다.

HTML 파일의 모든것이 document 객체로 담겨있는데 자바스크립트는 document 객체를 object 타입으로 가져와 내부의 값을 변경 할 수 있다.

사용 예시는 다음과 같다.

```jsx
document.title = "hello";
```

이렇게 한다면 HTML의 title태그에 내용이 있더라도 페이지의 제목이 hello로 바뀌게 된다.

document 내부에는 title, head, body 등 여러가지 태그가 object 타입으로 담겨있다.

## getElementById

---

`getElementById`는 HTML의 특정 개체를 가져오는 기능이다.

사용예시를 먼저 보자.

```html
<h1 id="title">hello</h1>
```

이런 HTML태그가 있다고 할 때

```jsx
document.getElementById("title");
```

이라면 HTML에서 태그의 id값(태그값 자체가 아니다! `<title>`태그와 혼동하지 말자)이 title인 태그를 가져온다.

```jsx
const h1Tag = document.getElementById("title");
h1Tag.innerText = "hi";
```

이처럼 변수에 저장해 객체처럼 사용 할 수도 있다.

## console.dir

---

`console.log`가 console에 로그를 찍어주는 역할이라면 `console.dir`은 이를 통해 가져온 태그 내부의 모든 정보를 object 타입으로 가져온다.

```jsx
console.dir(document);
```

이렇게 하면 document의 모든 정보가 object 타입으로 콘솔에 출력된다.

출력된 정보를 보고 수정, 추가, 삭제, 이벤트 등 여러방면으로 활용이 가능하다.

## querySelector

---

querySelector 역시 태그를 가져올수 있는태그이다.

먼저 사용 예제를 보자

```html
<div class="hello">
        <h1>hello!</h1>
</div>
```

```jsx
const h1 = document.querySelector(".hello h1");

console.log(h1)
```

각각의 HTML, JS코드가 있고 JS의 `querySelector` 를 통해 div태그 내부의 h1태그를 가져온 후 콘솔에 출력한 코드이다.

![콘솔에 태그를 출력한 모습](/images/javascript-img-3/Untitled.png)

만약 위 코드에 상응하는 값이 여러개라면 어떻게 되는지 한번 보자.

```html
<div class="hello">
        <h1>hello 1!</h1>
</div>
<div class="hello">
        <h1>hello 2!</h1>
</div>
<div class="hello">
        <h1>hello 3!</h1>
</div>
```

```jsx
const h1 = document.querySelector(".hello h1");

console.log(h1)
```

![첫번째 태그만 출력되는걸 볼 수 있다.](/images/javascript-img-3/Untitled%201.png)

결과는 한개만 나오며 제일 앞의 것이 출력되는것으로 나왔다.

모두 출력하고 싶을경우 `querySelectorAll`을 사용하면 된다.

`querySelectorAll`을 사용하면 결과는 리스트로 반환된다.

![결과가 리스트로 출력된다.](/images/javascript-img-3/Untitled%202.png)

코드에서 살짝 알수 있었듯이 `querySelector`는 CSS선택자를 지원한다. (예시에서의 .hello)

그래서 `title`을 쓸때 `#title`을 쓸때 `.title`을 쓸때 모두 다르며 각각 태그, ID, 클래스를 의미한다. 

## addEventListener

---

`addEventListener`는 이벤트를 감지하는 역할을 한다.

여기서 이벤트란 마우스를 움직이거나 키를 입력하거나 브라우저 창 크기를 조정하거나 텍스트를 복사하거나 와이파이연결을 해제하는등 PC의 대부분의 IO에 관한 모든것을 말한다.

다음은 사용예시이다.

```jsx
// 객체가 h1태그, 이름은 name, 함수이름은 func 라 가정
name.addEventListener("click", func);
```

위 코드가 뜻하는 바는 ‘name의 h1 태그를 클릭할 경우 func 함수를 실행한다.’ 이다.

코드에서 주의할 점이 있는데 func()가 아닌 그냥 func인 것이다.

func()를 하게되면 클릭이라는 조건이 갖춰지지 않아도 페이지 로딩중에 함수가 실행된다.

그렇기 때문에 함수는 괄호를 제외한 함수 이름만 입력해 주어야 한다.

여기서 `click`같은 조건을 더 많이 알고싶다면 구글링으로 (태그명) HTML event MDN 등을 검색하거나, `console.dir(객체)`를 통해 콘솔에서 더 찾아볼 수 있다. 객체의 내부 구성요소중 앞에 on이 붙은것들이 모두 이벤트라보면 된다.

이벤트 종류는 매우 많으니 다 외울수도 없을뿐더러 외울 필요도 없다.

파생형으로 `name.onclick = func;`이렇게 사용할 수도 있다.

그러나 `addEventListener`를 통해 이벤트를 감지한다면 이후 `removeEventListener`를 통해 event listener를 제거할 수도 있다.

필자는 `addEventListener`를 주로 사용할듯.