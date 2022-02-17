---
title: (JAVA) 제네릭(generic) 
date: 2022-02-17 14:47:05  

categories:
- Java

tags:  
- Java
- Generic
---


요즘 쓰는 포스팅의 주제는 항상 듣고있는 강의에서 나온다.  

강의에서는 제네릭을 직접 언급하지는 않았지만 List 자료형이나 Map 자료형들을 사용할때 제네릭 `<>` 을 사용한다.

제네릭을 알고는 있었지만 모양만 알고있었을뿐 용법과, 사용처에대해서는 몰랐기에 포스팅 작성을 통해 알아보려 한다.

## 제네릭(generic) 이란 ?

---

자바에서 제네릭이란 데이터의 타입(data type)을 일반화한다(generalize)는 것을 의미한다고 한다.

....

여전히 모호하다. 그래서 다른 글을 읽어본 결과

**클래스 / 인터페이스 / 메소드 에서 사용할 타입을 클래스 외부에서 설정하는 것** 이라고 한다.

그렇다면 제네릭을 사용하는 이유는 무엇일까

### 제네릭을 사용하는 이유

제네릭 타입을 사용함으로써 잘못된 타입이 사용될 수 있는 문제를 컴파일 과정에서 제거할 수 있기 때문이다.

자바 컴파일러는 코드에서 잘못 사용된 타입 때문에 발생하는 문제점을 제거하기 위해 제네릭코드에 대해 강한 타입 체크를 한다.

실행시 에러가 나는 것보다 컴파일 시 미리 강하게 체크하여 에러를 사전방지하는게 더 좋기 때문.

또 제네릭 코드를 사용하면 타입을 국한하기 때문에 요소를 찾아올 때 타입 변환을 할 필요가 없어 프로그램 성능이 향상된다.

- 강한 타입체크를 하여 에러를 사전방지하기 위함
- 타입 변환을 할 필요가 없게 타입을 국한하여 프로그램 성능 향상을 위함

## 제네릭의 사용

---

제네릭 타입은 타입을 매개변수로 갖는 클래스와 인터페이스를 말한다.

제네릭 타입은 클래스 또는 인터페이스 이름 뒤에 `<>` 부호가 붙으며 사이에 타입 파라미터가 위치한다.

```java
public class 클래스명<T> {}
public interface 인터페이스명<T> {}
```

타입 파라미터는 **정해진 규칙은 없으며**, 일반적으로 대문자 알파벳 한글자로 표현한다.

### 자주 사용하는 타입 파라미터

| 타입 파라미터 | 뜻 |
| --- | --- |
| `<T>` | Type |
| `<E>` | Element |
| `<K>` | Key |
| `<N>` | Number |
| `<V>` | Value |
| `<R>` | Result |

### 제네릭의 사용 예시

```java
public class exam<T> {

    List<T> examList = new ArrayList<>();

    public void method1(T input) {
        examList.add(input);
    }
}

class GenericClass {
    public static void main(String[] args) {
        exam<String> stringExam = new exam<>();

        exam<Integer> integerExam = new exam<>();
    }
}
```

exam 클래스는 <T>로 제네릭이 설정되어 있고 내부의 List타입의  examList 객체도 <T>로 제네릭 설정이 되어있다.

GenericClass 클래스는 두 개의 객체 stringExam과 intergerExam 이 있으며 두 객체의 타입은 `exam` 타입이다.

`exam` 타입은 선언부에 제네릭이 설정되어있으니 **사용하는 쪽에서도 제네릭 타입을 명시 해줘야 한다.**

이 코드에서는 각각 <String>과 <Integer>로 설정해주었다.

이제 stringExam객체는 타입이 String인 데이터만, integerExam객체는 타입이 int 인 데이터만 사용할 수 있다.

정말 그런지 확인을 해 보면

![](/images/Java-generic/Untitled.png)

stringExam.method1의 매개변수로 문자열을 주었을때는 컴파일에러가 발생하지 않다가

![](/images/Java-generic/Untitled%201.png)

문자열만 들어가야하는 List에 정수를 매개변수로 주니 컴파일 에러가 발생한다.

![](/images/Java-generic/Untitled%202.png)

반대의 경우도 마찬가지.

이와같이 제네릭을 사용할 경우 클래스 내부에서 사용하는 데이터의 타입을 지정할 수 있으며,

타입을 잘못 사용하여 발생하는 에러를 최소화 할 수 있다.

이는 회원가입폼의 ID란에서 특수문자를 사용하지 못하게 예외처리를 하는것과 비슷하다.

## 제네릭에 사용 가능한 타입

---


### 데이터 타입의 종류

여기서 간단히 데이터 타입의 종류와 특징을 알아보면

|  | 기본형 타입 | 참조형 타입 |
| --- | --- | --- |
| 종류 | - 정수형 : byte, short, int, long </br> - 실수형 : float, double </br> - 문자형 : char </br> - 논리 타입 : boolean | 기본형 이외의 모든 형태 </br> - 배열(array[]) </br> - 열거(enum) </br> - 클래스(class) </br> - 인터페이스(interface) |
| 특징 | - 직접 값을 넣을 수 있음 </br> - 스택 영역에 저장 | - 값들을 저장하고 있는 객체를 가르키는 ‘주소’를 넣을 수 있음 </br> - 힙 영역에 저장 |

그렇다면 제네릭에는 어떤 타입을 설정할수 있을까?

제네릭의 타입으로는 **참조형 데이터 타입**만 설정 가능하다.

int, byte, double, char 같은 기본형 데이터 타입은 설정할 수 없다.


?????

분명 우리는 위 코드에서 정수형데이터로 Integer가 입력이 되는것을 보았다.

Integer와 같은 형태를 **래퍼클래스**(wrapper class) 라고 한다.

래퍼클래스는 **기본형 데이터 타입을 참조형 데이터 타입으로 바꿔주는 클래스**다.

![기본형 데이터 타입의 래퍼클래스](/images/Java-generic/Untitled%203.png)

위 코드에서는 기본형인 int 가 아닌 래퍼클래스인 Integer를 사용함으로써 설정이 가능했던 것이다.

## Reference.

[제네릭(Generic) 사용법 & 예제 총정리](https://coding-factory.tistory.com/573) - 코딩팩토리

[제네릭의 개념](http://www.tcpschool.com/java/java_generic_concept) - TCP SCHOOL.com

[Java 제네릭(Generic) 이란??](https://2dubbing.tistory.com/17) - 비실이의 개발 성장기