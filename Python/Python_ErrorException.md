파이썬 예외처리
===
프로그래밍을 하면서 우리는 크고 작은 Error를 숱하게 만나게 된다. 이는 별로 달갑지 않은 결과이다. 
그 이유는 Error가 나면 결과적으로 우리가 의도한 로직을 구현할 수 없기 때문이다.  
이에 더해 더 큰 문제가 있다. Error가 나면 원하는 결과를 얻지 못할 뿐아니라 프로그램이 강제 종료된다.  
따라서 예외 처리의 의미는 에러 방지도 있지만, 에러가 발생하더라도 최소한 프로그램 종료는 방지하기 위함에 있다.
파이썬 코드를 실행 시 에러가 발생하면 파이썬 인터프리터(셀)가 해당 오류를 던진다(Throw).  
개발자는 던져질 오류에 대한 처리를 except문으로 구비해 놓아야 Error 예외 처리가 가능하다. 

파이썬 예외 처리 실습 (1): 기본 예외 처리
---
```python
try:
  실행코드 1
  실행코드 2
  ...
except[발생 가능한 에러 클래스]:
  실행코드 1
  실행코드 2

#1. 제대로 된 예상 오류 지정 시 : 에러 발생 X

>>> try:
...     4/0
... except ZeroDivisionError as zde:
...     print('0으로 나눌 수 없습니다')
... 
0으로 나눌 수 없습니다

#2. 다른 예상 오류 지정 시 : 에러 발생
>>> try:
...     4/0
... except FileNotFoundError as e:
...     print('파일을 찾을 수 없습니다')
... 
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
ZeroDivisionError: division by zero

#3. 디폴트 오류 (오류명생략) 지정시: 에러 발생 X
>>> try:
...     4/0
... except:
...     print('뭔지 모를 에러')
... 
뭔지 모를 에러
```
try 블록 내 실행코드들을 실행하던 중 에러가 발생하면 인터프리터는 해당 Error 클래스를 던진다.  
except 오른쪽에 해당 에러 클래스를 정의 해놓았다면 (catch) except 내 실행코드가 실행되고.  
정의하지 않았다면 에러가 나고 프로그램이 종료된다.  
위 코드에서 알 수 있듯 오류명을 기재하지 않으면 오류의 최상위 클래스인 Exception이 입력된다.  

파이썬 예외 처리 실습 (2): else와 finally 사용
---
else 문은 try 블록 내 에러가 발생하지 않을 경우 else: 블록 내 코드들이 실행된다.    
finally 문은 try 블록 내 에러 발생 여부에 상관 없이 무조건적으로 실행된다.  
```python
>>> try:
...     4/0
... except:
...     print('에러 발생')
... else:
...     print('에러 발생 안함')
... finally:
...     print('에러 나던 안나던 이건 실행')
... 
에러 발생
에러 나던 안나던 이건 실행
```
파이썬 예외 처리 실습 (3): 다중 에러 처리, 에러 클래스 생성, 의도한 에러 만들기
---
**다중 에러 처리하기**
```PYTHON
# 다중 에러 처리하기
>>> try:
...     a = [1,2]
...     print(a[3])
...     4/0
... except IndexError as ID:
...     print('인덱스 범위를 벗어납니다')
... except ZeroDivisionError as ZDE:
...     print('0으로 나눌 수 없습니다')
... 
인덱스 범위를 벗어납니다
```
분명 에러가 두 개가 발생할 것이고, 이에 대비해 두 가지의 예외 처리를 해놓았다.  
그런데 실행 결과는 IndexError 하나만 처리 되었다. 4/0 코드는 예외처리 되지 않은 것인가?  
아니다. 정확히는 4/0 코드는 실행조차 되지 않았다. print(a[3]) 코드에서 Indexerror가 나고,  
이에 따라 예외 처리한 print('인덱스 범위를 벗어납니다') 코드가 실행되고 종료된다.  
따라서 보통은 try except를 각 코드별로 따로 감싼다.  

**에러 회피하기**
```python
try:
  ...
except:
  pass
```
이렇게 코드를 짜면 에러 발생시 아무 처리도 안하지만 최소 프로그램 종료는 안된다!

**일부러 에러 발생시키기**
프로그래머에게 에러란 반드시 없애야 하는 적과 같은 존재이다.  
그런데 일부러 에러를 발생시킨다니??  
그치만 이 작업은 다분히 바른(?)쪽으로 의도된 코드이다. 함께 살펴보자  
```python
class Bird:
    def fly(self):
       raise NotImplementedError # 이 메소드를 implements하지 않을시 이 에러를 던진다.

class Eagle(Bird):
    pass
    
>>> eagle = Eagle()
>>> eagle.fly()
NotImplementedError 발생!

class Eagle(Bird):
    def fly(self):
        print('독수리 난다')

>>> eagle = Eagle()
>>> eagle.fly
독수리 난다
```
즉 일부러 NotImplementedError를 던짐으로써  
Bird 클래스를 상속받는 클래스는 반드시 fly 메소드를 오버라이딩 하라는 강한 규칙을 생성한 것이다.  

**오류 클래스 만들기**
```python
class MyError(Exception:
    pass
    
try:
    ...
except Myerror:
    print('만든 에러가 발생!')
```
