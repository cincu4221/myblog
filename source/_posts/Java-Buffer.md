---
title: (JAVA) BufferedReader와 BufferedWriter를 통한 입출력
date: 2022-02-19 10:15:32  

categories:
- Java

tags:  
- Java
- Buffer
- BufferedReader
- BufferedWriter
---

백준의 자바 알고리즘 문제를 풀어보던 중 버퍼를 활용한 입출력을 사용해야 하나는 문제가 있었다.

나는 자바에서 입출력이라고는 Scanner와 println()밖에 몰랐기에 버퍼를 통한 입출력은 사용해본적이 없었다.

찾아보니 버퍼 입출력이 스캐너보다 효율면에서 훨씬 낫다는것을 알게되었고, 그로인해 작업속도차이가 많이 난다는것도 알게되었다.

그래서! 이번 포스팅의 목표는 버퍼를 활용한 입출력에대해 알아보고 활용할 수 있을 정도로 공부하는게 목적이다.

## Buffer

---

**BufferedReader /** **BufferedWriter**는 Buffer에 있는 IO 클래스이다. 스캐너와 다르게 입력된 데이터가 바로 전달되지않고 중간에 버퍼링이 된 후에 전달된다. 출력도 마찬가지로 버퍼를 거쳐 간접적으로 출력장치로 전달되고, 시스템의 데이터 처리 효율성을 높여주며 버퍼스트림을 **InputStreamReader / OutputStreamWriter** 을 함께 사용하여 버퍼링을 하게 되면 입출력 스트림으로부터 미리 버퍼에 데이터를 갖다 놓기 때문에 보다 효율적인 입출력이 가능하다.

## BufferedReader

---

```java
BufferedReader bf = new BufferedReader(new InputStreamReader(System.in)); // 객체 생성
Stirng s = bf.readLine(); // 문자열의 경우
int i = Integer.parseInt(bf.readLine()); // 정수의 경우
```

객체 생성은 1라인에서 bf 라는 이름만 마음대로 바꾸면 된다.

입력은 문자열과 숫자가 받는 방식이 좀 다른데 `readLine()` 메소드의 결과가 문자열이기때문에 정수형 변수에 저장할 경우 `Integer` 로 형변환을 해주어야 한다.

주의할 점이 있다면 예외처리를 꼭 해주어야 한다는 점인데 보통은 `throws IOException` 을 통해 해결한다.

이렇게 하면 버퍼를 통해 읽어들인 문자열 or 숫자를 변수에 저장한 것이다.

## StringTokenizer

---

읽어들인 데이터는 Line 단위로만 나뉘어지기 때문에 공백단위로 데이터를 가공하려면 따로 작업을 해줘야 한다.

```java
String s = "123 456";
StringTokenizer st = new StringTokenizer(s); // 객체생성 및 s를 st의 인자로 전달            
String a = st.nextToken(); // 공백으로 나뉘어진 s의 123이 문자열로 a에 저장
int b = Integer.parseInt(st.nextToken()); // s의 456이 숫자로 b에 저장

String array[] = s.split(" "); // 공백마다 데이터를 끊어 배열에 저장함
```

위 코드에서 보이듯 StringTokenizer에 nextToken()함수를 사용하면 readLine()을 통해 입력받은 값을 공백단위로 구분하여 순서대로 호출할 수 있다.

다음으로는 String.split()함수가 있는데 문자열을 공백단위로 끊어 배열에 저장하는 방식이다.

## BufferdedWriter

---

일반적으로 문자를 출력할때에 System.out.println();을 사용한다. 

크지않은 양의 출력일 경우 성능차이는 체감하지 못할 수 있지만 출력이 많아진다면 입력과 마찬가지로 버퍼를 활용하는것이 효율적이다.

```java
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out)); // 객체생성
String s = "12345"; // 출력할 문자열
bw.write(s); // 버퍼에 "12345"가 담긴 s 문자열을 올린다.
bw.newLine(); // 줄바꿈
bw.flush(); // 버퍼에 있는 데이터를 모두 출력시킴
bw.close(); // 스트림을 닫음
```

BufferedWriter의 경우 버퍼를 잡아 놓았기 때문에 반드시 flush() / close() 를 반드시 호출하여 버퍼를 비우고 닫아주어야 한다.

또한, bw.write에는 System.out.print**ln**();과 같이 자동개행기능이 없기때문에 개행을 해주어야 할 경우에는 \n을 통해 따로 처리해주어야 한다.

## 사용 예제

---

백준에 있는 문제를 풀어보자.

![백준 문제번호 15552번 (빠른 A+B)](/images/Java-Buffer/Untitled.png)

```java
public static void main(String[] args) throws IOException {
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		int x = Integer.parseInt(bf.readLine());
		
		for (int i = 0; i < x; i++) {
				StringTokenizer st = new StringTokenizer(bf.readLine(), " ");
				bw.write((Integer.parseInt(st.nextToken()) + Integer.parseInt(st.nextToken())+ "\n");
		}
		bw.flush();
		bw.close();
}
```

라인 1 : throws IOException을 통해 버퍼 사용에 필요한 예외처리를 해줌

라인 2,3 : 버퍼 입출력 객체 생성

라인 5 : 정수형 변수에 반복횟수 지정을 위해 readLine()함수로 입력을 받고 정수형으로 형변환

라인 8 : st변수명으로 StringTokenizer 객체 생성과 동시에 입력을 공백으로 나누어 받음

라인 9 : 버퍼에 라인 8에서 입력된 나눠진 문자열을 첫번째와 두번째 것만 정수로 변환한 뒤 더하고 그 값을 버퍼에 올린다. 이후 \n으로 버퍼내부에서 개행

라인 11 : 반복문을 통해 버퍼에 작성된 데이터를 모두 출력한다.

라인 12 : 스트림을 닫는다.

---

스캐너보다는 다소 복잡하다. 그래도 속도면에서 확실한 이점이 있다고 하니 버퍼 사용에 익숙해지는것이 좋을 것 같다.

## Reference.

**[[Java] BufferedReader, BufferedWriter를 활용한 빠른 입출력](https://coding-factory.tistory.com/251) - 코딩팩토리**