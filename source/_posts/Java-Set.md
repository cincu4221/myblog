---
title: (JAVA) 집합 (Set) 자료형
date: 2022-02-05 12:40:43  
categories:   
- JAVA 

tags:
- JAVA
- Set
---


Map자료형에 대해 포스팅하던중 `keySet()` 메소드의 리턴값이 Set 자료형인걸 알게되었지만 난 그게 무슨 자료형인지 몰랐다.

자바에 자료형이 많은건지 기초공부를 제대로 안한건지 내가 모르는 자료형에는 Map과 Set외에도 Enum 등의 자료형이 있었다.

그래서 일단은 강의를 보면서 중간에 이해를 못하는일을 줄이기 위해 기본적인 자료형들의 사용법을 간단히 포스팅 하려 한다.

## 집합 자료형의 생성

---

집합 자료형은 아래 코드처럼 `HashSet`을 사용하여 만들 수 있다.

```java
import java.util.Arrays;
import java.util.HashSet;

public class SetExample {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>(Arrays.asList("H", "e", "l", "l", "o"));
        System.out.println(set); // [e, H, l, o] 출력
    }
}
```

`Set` 자료형 역시 `Map` 자료형 처럼 인터페이스이며, Set 인터페이스를 구현한 자료형에는 HashSet, TreeSet, LinkedHashSet 등이 있다.

## 집합 자료형의 특징

---

분명 H,e,l,l,o 가 들어있는 배열로 HashSet 자료형을 만들었으나 출력을 보면 l 한개가 빠져있고 순서도 뒤바뀌어 있다.

그 이유는 집합자료형에는 다음과 같은 특징이 있기 때문이다.

- 중복을 허용하지 않음
- 순서가 없음

리스트나 배열은 순서가 있으므로 인덱싱을 통해 자료형의 값을 얻을수 있지만 Map과 Set 자료형은 순서가 없기때문에 인덱싱으로 값을 얻을 수 없다.

## 교집합, 합집합, 차집합 구하기

---

교집합, 합집합, 차집합을 구하기 위해 일단 중복되는 숫자가 있는 각각의 배열로 Set 자료형을 2개 만든다.

```java
import java.util.Arrays;
import java.util.HashSet;

public class SetExample {
    public static void main(String[] args) {
        HashSet<Integer> set1 = new HashSet<>(Arrays.asList(1,2,3,4));
        HashSet<Integer> set2 = new HashSet<>(Arrays.asList(3,4,5,6));
    }
}
```

### 교집합

```java
HashSet<Integer> inter = new HashSet<>(set1); // set1 으로 inter 생성
inter.retainAll(set2); // 교집합 수행
System.out.println(inter); // [3, 4] 출력
```

위에서 만든 set1과 set2의 교집합을 구하는 방법이다.

set1이 있던 inter에 `retainAll` 을 통해 set2를 교집합해주니 원본이 사라지고 교집합의 결과가 inter가 되었다.

### 합집합

```java
HashSet<Integer> union = new HashSet<>(set1);
union.addAll(set2); // 합집합 수행
System.out.println(union); // [1, 2, 3, 4, 5, 6] 출력
```

합집합을 구하는 방법.

set1으로 union을 만들고 `addAll` 의 인자로 set2를 주면 union의 원본이 사라지고 합집합의 결과가 union에 저장된다.

### 차집합

```java
HashSet<Integer> sub = new HashSet<>(set1);
sub.removeAll(set2); // 차집합 수행
System.out.println(sub); // [1, 2] 출력
```

차집합을 구하는 방법.

set1 으로만든 sub에 `removeAll` 의 인자로 set2를 주면 sub의 원본이 사라지고  sub와 set2의 차집합의 결과가 sub에 저장된다.

## 집합 자료형 관련 메소드

---

### 값 추가하기(add)

집합 자료형에 값을 추가할 때 add 메소드를 사용한다.

```java
import java.util.HashSet;

public class SetExample {
    public static void main(String[] args) {
        HashSet<String> addSet = new HashSet<>();
        addSet.add("마우스");
        addSet.add("키보드");
        addSet.add("스피커");
        System.out.println(addSet); // [스피커, 키보드, 마우스] 출력
    }
}
```

### 값 여러개 추가하기(addAll)

여러개의 값을 한꺼번에 추가 할 때 addAll 메소드를 사용한다.

```java
import java.util.Arrays;
import java.util.HashSet;

public class SetExample {
    public static void main(String[] args) {
        HashSet<String> addAllSet = new HashSet<>();
        addAllSet.add("마우스");
        addAllSet.addAll(Arrays.asList("마이크", "모니터"));
        System.out.println(addAllSet); // [마이크, 모니터, 마우스] 출력
    }
}
```

합집합을 구할때의 `addAll` 사용법과 같다.

### 특정 값 제거하기(remove)

특정 값을 제거하고 싶을 때는 다음과 같이 remove 메소드를 사용한다.

```java
import java.util.Arrays;
import java.util.HashSet;

public class SetExample {
    public static void main(String[] args) {
        HashSet<String> removeSet = new HashSet<>(Arrays.asList("마이크", "모니터", "마우스"));
        removeSet.remove("모니터");
        System.out.println(removeSet); // [마이크, 마우스] 출력
    }
}
```

이 포스팅은 아래의 출처를 필사하여 작성한 포스팅입니다.

## Reference.

[점프 투 자바 3-9 집합(Set)](https://wikidocs.net/157108) - 박응용