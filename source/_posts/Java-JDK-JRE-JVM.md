---
title: (JAVA) 자바 플랫폼 3대 구성요소 (JDK, JRE, JVM)  
date: 2022-02-14 11:49:37  

categories:
- Java

tags:  
- Java
- JDK
- JRE
- JVM
- stub
---

자바, 스프링 강의를 듣거나 책을 보다보면 JDK, JRE, JVM에 대한 내용이 가끔 나온다.  
강의에서 나올때마다 자바의 필수요소인가보다 하며 지나쳤었지만 이번 포스팅을 통해 짚어보고 넘어가려 한다.


## JDK (자바 개발 키트, Java Development Kit)

---
### JDK란
> 자바 플랫폼의 등장 이래 지금까지  가장 널리 사용되고 있는 소프트웨어 개발 키트(SDK) - 위키백과

즉, Java로 소프트웨어를 개발할 수 있도록 여러 기능들을 제공하는 패키지이다.

### JDK의 구성
Java로의 개발을 담당하는 패키지답게 매우 많다. 자주 들어본것만 간추려보자면

- javac : 자바 컴파일러, 자바 소스파일(.java)을 바이트코드(.class)로 변환한다.
- java : javac가 만든 클래스 파일을 해석 및 실행한다.
- jar : 서로 관련있는 클래스 라이브러리들과 리소스를 하나의 파일로 묶어주는 도구이다.
- JDB : Java Debugger, 자바 디버깅 툴
- JRE (Java Runtime Environment) : Java가 동작하는데 필요한 JVM, 라이브러리 등 다양한 파일들을 포함한다. Java를 실행시키기 위해필요하다.
- JVM(Java Virtual Machine) : Java가 실제로 동작하는 가상환경. JVM 덕분에 하나의 소스파일을 만들더라도 여러 환경(OS) 에서 원활히 동작이 가능하다.

### JDK의 종류
1. **Java SE : Standard Edition**  
표준 자바 플랫폼으로 표준적인 컴퓨팅 환경을 지원하기 위한 자바 가성머신 규격 및 API 집합을 포함한다.  
이후의 Java EE, Java ME는 구체적인 목적에 따라 Java SE를 기반으로 API를 추가하거나 자바 가상머신 규격 및 API의 일부를 택하여 정의 된다.
2. **Java EE : Enterprise Edition**
Java SE에 웹 어플리케이션 서버에서 동작하는 기능을 추가한 플랫폼  
이 스펙에 따라 제품을 구현한 것을 웹 어플리케이션 서버( [WAS](http://sungbine.github.io/tech/post/2015/02/15/tomcat%EA%B3%BC%20apache%EC%9D%98%20%EC%97%B0%EB%8F%99.html) )라 한다.(톰캣 등)
3. **Java ME : Micro Edition**
제한된 자원을 가진 휴대전화, PDA 등에서 Java 프로그래밍 언어를 지원하기 위해 만든 플랫폼 중 하나이다.

## JRE (자바 런타임 환경, Java Runtime Environment)

---
컴파일된 자바 프로그램을 실행시킬 수 있는 자바 환경을 말한다.
자바 프로그램을 실행시키기 위한 라이브러리, JVM, 기타 파일들을 포함하고있다.
자바 프로그램을 실행시키기 위해서는 JRE를 반드시 설치해야하고 JRE에는 개발과 관련된 도구는 포함되어 있지 않다.

## JVM (자바 가상 머신, Java Virtual Machine)

---
JVM은 Java Virtual Machine(자바 가상머신)의 약자로 자바 소스코드로 만들어지는 자바 바이트코드 파일을 실행할 수 있다.  
JVM은 자바와 다르게 플랫폼에 의존적므로 맥, 윈도우, 리눅스의 JVM은 각각 다르다.  
하지만 컴파일된 바이트코드 파일은 어떤 JVM에서도 동작시킬 수 있다. 즉, 코드를 작성하면 JVM이 설치된 어떤 플랫폼에서도 동작시킬수 있다.

JVM의 역할은 다음과 같다.
- 바이트코드를 읽는다.
- 바이트코드를 검증한다.
- 바이트코드를 실행한다.
- 실행환경(Runtime Environment)의 규격을 제공한다. (필요한 라이브러리 및 기타파일)


마지막으로 각각의 관계를 살펴보면 다음 그림과 같다.  
![JDK, JRE, JVM의 관계](/images/Java-JDK-JRE-JVM/img_1.png)








## Reference.
[자바 개발키트 위키백과](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EA%B0%9C%EB%B0%9C_%ED%82%A4%ED%8A%B8)  
[[Java] Java SE, JDK, JRE](https://devbox.tistory.com/entry/%EC%8B%A4%ED%96%89)