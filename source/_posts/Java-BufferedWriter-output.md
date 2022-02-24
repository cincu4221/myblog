---
title: (JAVA) BufferedWriter.write() 의 출력 타입
date: 2022-02-24 14:03:18  

categories:
- Java

tags:  
- Java
- Buffer
- BufferedReader
- BufferedWriter
---


버퍼를 요 며칠간 써보고 있지만 아직 스캐너를 쓸 때에 비해서는 익숙치 않다.

그러던 중 백준의 알고리즘 문제를 풀면서 `BufferedWriter.write()` 함수를 사용할 때 마다 숫자가 아스키코드로 출력되어 문제가 되었다.

## 문제

예시를 한번 보자면

```sql
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int x = Integer.parseInt(bf.readLine());

        for (int i = x; i > 0; i--) {
            bw.write(i);
            bw.newLine();
        }
        bw.flush();
        bw.close();
    }
}
```

숫자를 입력하면 그 숫자부터 1까지 -1되며 출력되는 매우 간단한 코드이다.

그런데 실행하면 다음과 같이 출력된다.

![](/images/Java-BufferedWriter-Output/Untitled.png)

분명 5를 입력했으니 5부터 1까지 차례로 출력되어야 하지만 글자가 깨져 출력되고있다.

![](/images/Java-BufferedWriter-Output/Untitled%201.png)

이는 숫자 자체가 아닌 5에서 1까지 해당하는 아스키코드가 대응하여 출력되었기 때문이다.

![](/images/Java-BufferedWriter-Output/Untitled%202.png)

아스키코드에서 ! 인 33을 입력하면 !와 32인 공백문자가 출력되는걸 볼 수 있다.

## 원인

원인은 `bw.write(i)` 부분에서 정수 타입인 i를 그대로 출력하려고 했기 때문이다.

## 해결

정수형을 그대로 출력하려고 했을때 문제가 발생했기에 형변환을 해주어야 한다.

따라서 정수 타입 변수를 버퍼를 통해 출력하고 싶으면 **문자열**로의 형변환이 필요하다.

```sql
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int x = Integer.parseInt(bf.readLine());

        for (int i = x; i > 0; i--) {
            bw.write(String.valueOf(i));
            bw.newLine();
        }
        bw.flush();
        bw.close();
    }
}
```

`bw.write(i)` 처럼 정수형으로 바로 출력하는 대신 `bw.write(String.valueOf(i))` 처럼 문자열로 형변환하면 다음처럼 출력이된다.

![- 편안 -](/images/Java-BufferedWriter-Output/Untitled%203.png)