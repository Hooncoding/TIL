파이썬 내장함수
===
파이썬은 고맙게도 자주 사용하는 함수들을 내장 함수(인터프리터에 이미 import 해놓음)로 구비해놨다.  
따라서 이 함수들은 우리가 따로 import 하지 않아도 사용할 수 있다.  
이 함수들이 내장되어 있는 이유는 그만큼 많이 쓰이기 때문이다. 따라서, 우리는 내장 함수를 잘 숙달해야 한다.  

파이썬 내장함수 알아보기
---
**abs(숫자형 객체)**  
숫자형 객체의 절댓값을 반환한다.

```python
>>> abs(-1)
1
```

**all(Iterable한 객체 x)**  
x내 요소가 모두 참이면 True, 거짓이 하나라도 있으면 False 반환

```python
>>> all(['a','b','','d'])
False
```

**any(Iterable한 객체 x)**
x내 요소들 중 하나라도 참이면 True, 모두 거짓이면 False 반환

```python
>>> any(['','','a',''])
True
```

**chr(integer)**
아스키 코드 중 입력된 정수에 해당하는 문자 반환 

```python
>>> chr(65)
'A'
```

**dir(Object)**
객체가 자체적으로 가지고 있는 변수나 함수를 보여준다.  

```python
>>> a = 3
>>> dir(a)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'as_integer_ratio', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
```

**divmod(나뉘는수, 나누는수)**
나눗셈의 몫과 나머지를 튜플로 반환

```python
>>> divmod(7,3)
(2, 1)
```

**enumerate(Iterable x)**
x의 각요소의 인덱스-요소값 쌍을 튜플로 반환

```python
>>> for i in enumerate([1,2,3,4]):
...     print(i)
... 
(0, 1)
(1, 2)
(2, 3)
(3, 4)
```

**eval(str)**
실행 가능한 문자열을 직접 실행

```python
>>> eval('1+2')
3
```

**filter(함수명, Iterable x)**
filter 함수의 실행과정은 다음과 같다.
1. 입력한 함수에 x 내 요소들을 하나씩 넣는다.
2. 요소가 함수를 타고 나온 결과가 나온다 (반드시 T/F, 필터의 인자로 쓰이는 함수의 return은 반드시 T/F)
3. 결과가 True인 요소만 filter 객체로 저장된다.

```python
# 리스트 중 0이 아닌 숫자만 추출한 새로운 리스트 만들기
>>> def iszero(num):
...     if num != 0:
...             return True
...     else:
...             return False
... 
>>> b = filter(iszero, [1,0,2,0,3,0,4,0])
>>> list(b)
[1, 2, 3, 4]
```

**hex(integer)**
입력 받은 정수의 16진수를 반환

```python
>>> hex(256)
'0x100'
```

참고: 16진수가 필요한 이유
--


