파이썬 매직 메소드
====
파이썬에는 매직 메소드라는 특이한 메소드가 존재한다.  
매직 메소드란 오브젝트 내 내장되어 있다.  
즉, 클래스에 따로 선언하지 않아도 사용할 수 있는 메소드 이다.  
대표적인 매직 메소드로는 우리가 주로 사용하는 '연산자'이다.  
예를 들어 + 연산자는 실제로는 __add__(self, other) 메소드를 호출하는 키워드이다.  
a + b 이라는 코드는 a.__add__(b)로 실행된다. self, other에는 주솟값이 들어가는데,    
위 코드에도 알 수 있 듯이 연산자 기준 왼쪽 객체의 주솟값이 self에, 오른쪽이 other에 들어간다.

``` python
>>> a = 1
>>> a.__add__(2)
3
```

매직 메소드 오버로딩
---
매직 메소드 역시 메소드이므로 오버로딩이 가능하다.  
이 의미는 + 연산자에 단순 더하기 기능에 더해 Customizing 할 수 있다.

```python
>>> class HousePark:
...     firstname = '박'
...     def __init__(self, name):
...             self.fullname = self.firstname + name
...     def __add__(self, other):
...             print('%s와 %s는 결혼합니다'%(self.fullname, other.fullname))
... 
>>> class HouseKim(HousePark):
...     firstname = '김'
... 
>>> gildong = HousePark('길동')
>>> chulsoo = HouseKim('철수')
>>> gildong + chulsoo
박길동와 김철수는 결혼합니다
```
원래 str + str은 두 str객체를 붙이기 기능을 했지만,  
이를 오버로딩하여 다른 방식으로 표현했다.  
