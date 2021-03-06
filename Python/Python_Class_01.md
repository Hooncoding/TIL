파이썬 클래스 (1): 클래스 선언, 객체 생성하기
======
파이썬에도 클래스가 존재한다.  
파이썬 내 클래스 선언에 앞서 클래스의 존재 이유에 대해 알아보자.  
클래스는 오브젝트를 생성하기 위한 템플릿(틀)이다.  
오브젝트를 생성학기 위해서는 일정한 형식이 필요한데 클래스가 그 역할을 한다.  
그렇다면 오브젝트는 왜 생성해야 할까?  
개발을 하다보면 반복적으로 쓰이는 변수나 메소드들이 있다.  
이들을 필요 시 마다 선언하여 사용하는 것은 비효율적 이다.  
따라서 자주 사용하는 변수나 메소드들을 클래스에 정의해놓고  
필요 시 해당 클래스를 new 하여 사용하기 위함이다.  
즉, 클래스의 필요 이유는 코드의 효율성을 높이기 위해서다.  

클래스 선언 및 오브젝트 생성하기 
----
**오브젝트 생성과 클래스 변수**
```python
>>> class TestClass:
...     msg = '테스트 클래스입니다'
... 
>>> testObject1 = TestClass()
>>> testObject2 = TestClass()
>>> testObject1.msg
'테스트 클래스입니다'
>>> testObject2.msg
'테스트 클래스입니다'
>>> TestClass.msg = '변수 변경'
>>> testObject1.msg
'변수 변경'
>>> testObject2.msg
'변수 변경'
```

여기서 msg 변수는 클래스가 소유한 변수라고 해서 클래스 변수라고 한다.  
클래스 변수는 해당 클래스를 new한 오브젝트들이 공유하는 변수이다.  
여기서 testObject 1/2의 msg는 같다.  
클래스 변수는 클래스의 소속이므로 object를 통해 클래스 변수의 변경은 불가능하다.

```python
>>> testObject1.msg = '클래스 변수 변경하기'
>>> TestClass.msg
'변수 변경'
```

**클래스 메소드 선언 및 활용**
```python
>>> class Calculator:
...     def sum(self, a, b):
...             result=a+b
...             return result
... 
>>> cal1 = Calculator()
>>> cal1.sum(1,2)
3
```

**self의 의미**
클래스 내 정의된 함수를 메소드라고 한다.  
파이썬 내 모든 메소드들의 첫 번째 인자는 self이다.  
이 self에 들어가야 할 인자의 자료형은 'object'이다.  
즉, self는 해당 메소드를 실행할 object의 주솟값이 들어가야 한다.  
그런데 위 코드에서는 self 자리에 아무런 값도 넣지 않았는데 정상 실행되었다.  
이는 self를 입력하지 않을 시 자동으로 메소드를 호출한 object가 입력된다.  
즉 위 메소드는 Calculator.sum(cal1,1,2)와 결과가 같다.  

**객체 변수 선언하기**
```python
>>> class naming:
...     name = '초기 이름'
...     def setName(self, name):
...             self.name = name
... 
>>> hong = naming()
>>> hong.name 
'초기 이름'
>>> hong.setName('홍길동')
>>> hong.name
'홍길동'
>>> kim = naming()
>>> kim.setName('김철수')
>>> kim.name
'김철수'
```
클래스 변수 뿐 아니라 각 객체마다 사용할 객체 변수 역시 만들 수 있다.
self 인자를 사용하여 객체 변수를 선언할 수 있는데
self는 메소드를 호출한 object를 가리키므로 object.name 즉, 객체의 name이란 변수를 세팅한다.  

**NameSpace 개념**  

다음 예제를 살펴보자
```python
>>> class naming:
...     name = '초기 이름'
...     def setName(self, name):
...             self.name = name
... 
>>> hong = naming()
>>> hong.setName('홍길동')
>>> hong.name
>>> hong.age = 20
>>> hong.age
20
```
분명 naming 클래스 내 age라는 변수가 없음에도 불구하고  
hong.age라는 변수를 선언했고 실제 실행 결과 제대로 20이라는 값이 반환됐다.  
이는 파이썬의 핵심 기능 중 하나인 NameSpace로 인해 가능해진 결과다.  
오브젝트를 생성 시 해당 오브젝트가 참조하는 클래스 내 변수, 메소드 명이
해당 오브젝트의 NameSpace에 저장된다.
즉, hong이라는 오브젝트의 NameSpace에는 name, setName이 저장된다.  
그런데 hong.age라는 코드를 실행할 경우 다음과 같은 절차가 실행된다.
1. hong 오브젝트의 NameSpace에 age라는 항목이 있는지 확인한다.
2. 있을 경우 age라는 항목에 대입값을 저장한다. 없을 경우 age라는 변수를 만들고 대입값을 저장한다.  

즉, 이렇게 되면 굳이 setName이라는 메소드가 필요없이 다음 코드로 같은 결과가 나온다.

```python
>>> class naming:
...     pass
... 
>>> hong.name = '홍길동'
>>> hong.name
'홍길동'
```
클래스 내 아무런 변수가 없다. 따라서 hong 생성시 NameSpace에는 아무런 항목도 없다.
hong.name 코드 실행 시 NameSpace에 name 항목이 없으므로 name이라는 변수를 만들고
'홍길동'이라는 대입값을 대입한다.
