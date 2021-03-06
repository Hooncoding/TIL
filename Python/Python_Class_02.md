파이썬 클래스 (2): 생성자 사용 및 클래스 상속
===
파이썬에서는 __init__메소드를 이용하여 생성자 기능을 사용할 수 있다.  
생성자란 오브젝트 생성 시 특정 변수의 값을 초기화 하는 것이다.  

생성자 사용하여 오브젝트 생성하기
---
생성자를 이용하면 특정 변수의 초기화를 하여 오브젝트를 생성한다고 했다.  
이 기능이 왜 필요할까?  
우선 편리함이다. 예를 들어 클래스 내 name이라는 변수에 이름을 입력하려면  
생성자 없이는 setName과 같은 메소드를 만들어 놓아야 한다.  
생성자를 사용하면 이러한 과정이 필요없다.  
다음으로 강제성이다. 어떤 오브젝트를 만들 때 name이라는 변수에 반드시 값이 들어가야 한다면  
name에 들어갈 값을 입력하지 않고서는 오브젝트를 생성할 수 없도록 만들면 된다.  
생성자를 만들면 해당 기능을 할 수 있다.  

다음 예제를 보자.  

```python
>>> class Service:
...     def __init__(self, name):
...             self.name = name
...     def sum(self, a, b):
...             result = a + b
...             print('%s님 %d + %d는 %d입니다.'%(self.name, a, b, result))
... 
>>> hong = Service()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __init__() missing 1 required positional argument: 'name'
>>> hong = Service('홍길동')
>>> hong.sum(1,2)
홍길동님 1 + 2는 3입니다.
>>> 
```

생성자를 선언한 이후로는 아무런 인자 없이 객체를 생성할 수 없다. (강제성 부여)  
hong.Service()가 불가능한 것이다. 따라서 hong.Service() 내 적절한 인자를 넣어줘야 한다.  
생성자를 사용하여 setName과 같은 메소드 없이도 '홍길동'이라는 이름이 객체 변수에 저장되었다. 

**잠깐! Attribute의 개념**
Attribute는 직역하면 속성이다.  
프로그래밍에서 Attribute는 get과 set 할 수 있는 변수를 의미한다.  
즉, 여기서 name이란 변수는 Attribute이다.  
인스턴스 변수(객체 변수)는 Attribute이다. 

클래스 상속
---
박씨 가문에서 이름 짓기, 여행 정보를 알려주는 다음과 같은 프로그래밍을 했다.
```python
>>> class HousePark:
...     lastname = '박'
...     def __init__(self, name):
...             self.fullname = self.lastname + name
...     def travel(self, location):
...             print('%s는 %s로 여행갑니다'%(self.fullname, location))
... 
>>> gildong = HousePark('길동')
>>> gildong.fullname
'박길동'
>>> gildong.travel('서울')
박길동는 서울로 여행갑니다
```

이 서비스를 샘내던 김씨 가문은 HousePark을 상속하여 재사용하려고 한다.  
이 경우 간단하게 이렇게 코딩하면 된다.
```python
>>> class HouseKim(HousePark):
...     lastname = '김'
... 
>>> chulsoo = HouseKim('철수')
>>> chulsoo.fullname
'김철수'
>>> chulsoo.travel('부산')
김철수는 부산로 여행갑니다
```

단지 상속만 받은 후 lastname 변수만 바꿨을 뿐인데 김씨 이름으로
HousePark의 모든 기능을 사용할 수 있게 되었다.

**메소드 오버라이딩**
김씨 가문은 단순히 HousePark 클래스를 사용할 뿐아니라 이를 재정의 하려고 한다.  
상속한 클래스와 같은 이름의 메소드의 코드를 변경하여 사용하는 것을 오버라이딩이라고 한다.
```python
>>> class HouseKim(HousePark):
...     lastname = '김'
...     def travel(self, location):
...             print('%s는 %s에 비행기를 타고 갑니다'%(self.fullname, location))
... 
>>> chulsoo = HouseKim('철수')
>>> chulsoo.travel('부산')
김철수는 부산에 비행기를 타고 갑니다
```
이제 김씨 가문 사람들(Object)는 travel 함수 호출시 '비행기를 타고' 간다. 
