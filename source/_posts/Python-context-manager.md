---
title: 파이썬(Python) with 구문
date: 2021-12-06 19:33:41  
categories: 
- Python

tags:
- Python
- Context manager
---

## with 구문이 무엇인가?

---
보통 프로그램은 파일에 접근해서 파일 내용등을 읽고 쓰고 수정하는등의 일을 수행한 뒤 다시 그 파일을 마운트 해제 하는 패턴을 따른다.  
예시로 사용자가 워드파일 문서 작업을 하고 있을 때 그 파일을 열고있는 동안 파일관리자가 그 문서의 이름을 바꾼다던지 파일의 경로를 변경한다던지 같은 파일에 접근을 필요로하는 행동을 타 프로그램에서 할 수 없게 된다.

결론만 말하자면 파일에 접근했으면(열었으면) 해제하는(닫아주는) 일을 빼먹지 않고 해주어야 한다는 것이다.  
보통 close() 같은 메소드를 사용하여 파일을 닫아주지만 이는 문제점이 있다.  
파일 처리를 수행하는 도중에 오류가 발생하게되면 아래에있는 close() 문을 실행할 수 없고 파일을 닫을수 없게된다.  

with 문은 그 구문을 실행했을 때 오류가 발생하던 하지않던 마지막에 close 를 해주도록 하는 것이다.

## with문 사용 예시

---
```python
# 일반적인 코드
file = open('textfile.txt', 'r')
contents = file.read()
file.close()

# try finally를 사용한 코드
try:
    file = open('textfile.txt', 'r')
    contents = file.read()
finally:
    file.close()
    
# with 구문을 사용한 코드
with open('textfile.txt', 'r') as file:
    contents = file.read()
```
위의 세가지 코드는 모두 같은 내용이지만 첫번째 코드를 실행할때 contents = file.read() 행에서 에러가 난다면 file.close()를 실행하지 못해 파일을 닫을 수 없다.  
그러나 아래의 두가지 코드는 에러가 발생해도 코드를 닫을 수 있을 뿐더러 with문은 더욱 간결하여 보기 편하다.


<br><br>
## 여러개의 파일 관리하기

---

두 개 이상의 파일을 동시에 사용할 때 with as 문을 사용하는 방법이다.  
두개의 with as 문을 겹쳐도 되고, 하나의 with문에 두 개 이상의 파일을 열어도 된다.
```python
with open('textfile_a.txt', 'r') as a:
    with open('textfile_b.txt', 'w') as b:
        a_file = a
        b_file = b.write('hello wolrd')
        
with open('textfile_a.txt', 'r') as a, open('textfile_b.txt', 'w') as b:
        a_file = a
        b_file = b.write('hello world')

# 파이썬 3.10.0 b1 버전부터는 아래처럼도 가능하다
with (
    open('textfile_a','w') as a,
    open('textfile_b','w') as b,
    open('textfile_c','w') as c
):
    a.write('apple')
    b.write('banana')
    c.write('count')
```
## class로 context manager 구현하기

---
```python
class File(object):
    def __init__(self, file_name, method):
        self.file_obj = open(file_name, method)
    def __enter__(self):
        return self.file_obj
    def __exit__(self, type, value, trace_back):
        self.file_obj.close()
```
위와 같이 정의를 하고 아래처럼 실행해 보면
```python
with File('demo.txt', 'wb') as opened_file:
    opened_file.write('Hola!')
```
1. with 문은 File class의 __exit__메소드를 저장
2. File class의 __enter__메소드를 호출
3. __enter__메소드는 파일을 열고 파일을 반환
4. 열려진 파일은 변수명 opened_file에 저장
5. .write()을 통해 내용 작성
6. with문 이기 때문에 __exit__문을 호출
7. __exit__문을 통해 파일 닫음

위와같은 실행순서로 context manager를 구현 할 수 있다.

## References.
https://tempdev.tistory.com/22  
https://ddanggle.gitbooks.io/interpy-kr/content/ch24-context-manager.html