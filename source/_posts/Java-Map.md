---
title: (JAVA) 맵 (Map) 자료형
date: 2022-02-04 11:06:52  
categories:   
- JAVA 

tags:
- JAVA
- Map
- HashMap
---


스프링 강의를 듣던중 Map이라는 자료형에 대해 처음으로 접했었는데 어떻게 사용하는지, 문법이 무엇을 의미하는지 전혀 몰랐기 때문에 구글링으로 좀 알아볼 필요성이 생겼다.

| key | value |
| --- | --- |
| music | 음악 |
| water | 물 |

기본적으로 위의 표처럼 파이썬의 딕셔너리, 자바스크립트의 오브젝트같이 key값과 value의 대응관계로 구분된 자료형이다.

Map은 리스트나 배열처럼 인덱스를 통해 해당 요소의 값을 구하는 것이 아닌 key를 통해 value의 값을 얻는다.

## HashMap

---

Map은 인터페이스이며(필자는 포스팅하며 처음 알게되었다.) Map인터페이스를 구현한 Map자료형에는 HashMap, LinkedHashMap, TreeMap 등이 있다.

이번 챕터에서는 이들중 가장 간단한HashMap에 대해 알아본다.

### put

제네릭 `<>` 에서 선언한 타입으로 항목값을 입력할때 사용한다.

```java
import java.util.HashMap;

public class MapExample {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();
        map.put("music", "음악");
        map.put("water", "물");
    }
}
```

Map이 그렇듯 HashMap 역시 제네릭을 사용한다.

### get

key 값을 통해 value값을 얻을때 사용한다.

```java
System.out.println(map.get("music")); // 음악 출력
System.out.println(map.get("water")); // 물 출력
```

위처럼 get 메소드를 통해 key 값을 입력하면 대응하는 value값을 얻을 수 있다.

### getOrDefault

맵의 key에 해당하는 value가 없을때 get메서드를 사용하면 `null` 값이 리턴된다.

이 경우 `null` 대신 다른 디폴트 값을 얻고 싶다면 `getOrDefault` 메서드를 사용하면 된다.

```java
 System.out.println(map.getOrDefault("nation", "Korea")); // nation이 없기 때문에 'Korea' 리턴
```

### containsKey

`containsKey` 메소드는 Map에 해당 key가 있는지 확인후 그 결과값을 리턴한다.

```java
System.out.println(map.containsKey("music")); // key값이 있으므로 true
System.out.println(map.containsKey("nation")); // key값이 없으므로 false
```

### remove

remove 메소드는 Map의 항목을 삭제하는 메소드로 key값에 해당되는 항목(key, value)를 삭제한 후 그 value 값을 리턴한다.

```java
System.out.println(map.remove("music")); // 음악 출력
```

`map` 객체에 있던 “music”와 “음악”항목이 사라지고  “음악”이 리턴 될 것이다.

### size

size 메소드는 Map 항목의 갯수를 리턴한다.

```java
System.out.println(map.size()); // 1 출력
```

“music”, “water” 두개의 항목이 있었으나, `remove` 로 “music”을 삭제했으니 1이 출력 될 것이다.

### keySet

keySet은 Map의 모든 key를 모아서 리턴한다.

```java
import java.util.HashMap;

public class MapExample {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();
        map.put("music", "음악");
        map.put("water", "물");

        System.out.println(map.keySet()); // [music, water] 출력
    }
}
```

이때 리턴되는 자료형은 `Set` 자료형이며, `list` 자료형과는 다르지만 변환하여 사용이 가능하다.

## Reference.

[점프 투 자바 3-8 맵(Map)](https://wikidocs.net/208) - 박응용