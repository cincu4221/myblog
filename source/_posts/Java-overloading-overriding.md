---
title: (JAVA) 오버로딩, 오버라이딩 차이점  
date: 2022-01-31 14:31:25  
categories:   
- JAVA 

tags:
- JAVA
---

자바를 공부하다가 오버로딩(Overloading)과 오버라이딩(Overriding)이란 용어가 나와 헷갈릴수 있겠다 싶어 차이점을 찾아보고 포스팅 하려 한다.

## 오버로딩(Overloading)

---

### 오버로딩이란

같은 이름을 갖고있지만, 매개변수가 서로 다른 형식인 생성자, 메소드를 새로 정의하는 것.

### 오버로딩의 조건

- 메소드의 이름이 같아야 한다.
- 각 메소드 매개변수의 개수, 타입이 달라야 한다.

### 오버로딩의 예제

<코드>

```java
public class example {

    //메서드 오버로딩
    public void method1() {
        System.out.println("매개변수가 없는 매서드");
    }

    void method1(String var) {
        System.out.println("매개변수 문자열 " + var);
    }

    void method1(int value) {
        System.out.println("매개변수 정수타입 " + value);
    }

}

class exampleRun {

    public static void main(String[] args) {

        example ex = new example();
        ex.method1();
        ex.method1("안녕하세요");
        ex.method1(12345);

    }
}
```

<출력>

```
매개변수가 없는 매서드
매개변수 문자열 안녕하세요
매개변수 정수타입 12345
```

위 코드에서는 메소드만 오버로딩하였지만 생성자도 오버로딩하여 사용이 가능하다.

코드에서 확인할수 있는 것이 접근제한자가 달라도 오버로딩이 된다는 것이다.

오버로딩의 장점을 살펴보면  다음과 같다.

- 다형성 구현
- 소스코드 가독성 증가
- 메소드 이름 절약

## 오버라이딩(Overriding)

---

### 오버라이딩이란

상속 관계에 있는 부모 클래스에서 이미 정의된 메소드를 자식클래스에서 같은 이름을 가진 메소드로 다시 정의하는 것.

### 오버라이딩의 조건

- 메소드의 선언부가 기존메소드와 같을것
- 접근제한자를 부모클래스의 메소드보다 더 좁은범위로 변경 불가
- 부모클래스의 메소드보다 더 큰 범위의 예외 선언 불가

### 오버로딩의 예제

<코드>

```java
class parent {
    void method1() {
        System.out.println("이것은 부모클래스의 메소드입니다.");
    }
}

class child extends parent {
		@Override
    void method1() {
        System.out.println("이것은 자식클래스의 메소드입니다.");
    }
}

class childExample {
    public static void main(String[] args) {
        parent pa = new parent();
        pa.method1();
        child ch = new child();
        ch.method1();
        parent fa = new child(); // 자동 타입변환
        fa.method1();
    }
}
```

<결과>

```
이것은 부모클래스의 메소드입니다.
이것은 자식클래스의 메소드입니다.
이것은 자식클래스의 메소드입니다.
```

### `@Override` 는 무엇인가?

`@Override` 는 어노테이션(Annotation)이라는 기능으로 오버라이딩된 메소드의 위에 추가해주면 정상적으로 오버라이딩 되었는지 검증해주는 역할을 한다.

## 오버로딩, 오버라이딩의 차이점 정리

---

오버로딩은 새로운 메소드를 추가하는 것이고, 오버라이딩은 상속받은 메소드를 다시 정의하는 것이다.

이를 표로 나타내면 다음과 같다.

|  | 오버로딩(Overloading) | 오버라이딩(Overriding) |
| --- | --- | --- |
| 매개변수 | 달라야 한다. | 같아야 한다. |
| 메소드명 | 같아야 한다. | 달라야 한다. |
| 리턴형 | 달라도 된다. | 같아야 한다. |
| 접근제한자 | 모든 접근제한자 사용 가능 | 부모클래스의 접근제한자보다 더 넓거나 같은범위의 접근제한자만 가능 |
| 적용 범위 | 동일 클래스 내에서 적용된다. | 상속관계에서 적용된다. |