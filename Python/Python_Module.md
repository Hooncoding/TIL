파이썬 모듈
===
파이썬에서 모듈은 하나의 파일(파일명.py)을 의미한다.  
모듈 내에는 클래스, 메소드, 변수가 저장될 수 있으며, 이를 import할 경우  
해당 모듈 내 클래스, 메소드, 변수를 현재 작업하는 파일에서 사용할 수 있다.  

모듈 Import 하기
---
```python
# mod1.py
>>> def safe_sum(a,b):
...     if type(a) != type(b):
...         print('더할 수 없습니다')
...         result = 0
...         return result
...     else:
...         result = a + b
...         return result
... 
>>>

#import_mod1.py
>>> import mod1 as mod
>>> mod.sum(1,2)
3
>>> mod.safe_sum(1,'이')
더할 수 없습니다
0
```
import_mod1.py에서 mod1을 import한 이후 mod1.py 내 메소드를 사용해보았다.  
이때 임포트하는 파일명이 긴 경우 as를 주어 간단히 사용할 수 있다.  

다양한 방식으로 import 하기
---
위 mod1.py를 다양한 방법으로 import 해보자
```python
# import_mod1.py

# 1번 방법: 모듈 자체를 가져오기
>>> import mod1 as mod
>>> mod.sum(1,2)
3
>>> mod.safe_sum(1,'이')
더할 수 없습니다
0

# 2번 방법: 모듈 내 특정 메소드만 가져오기
>>> from mod1 import sum
>>> sum(3,4)
7
>>> safe_sum(1,'이')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'safe_sum' is not defined

# 3번 방법: 모듈 내 모든 요소 가져오기
>>> from mod1 import *
>>> sum(3,4)
7
>>> safe_sum(3,5)
8
>>>
```

모듈 내 특정 코드 제거하여 import하기
---
모듈을 만들고 나서 해당 모듈 내 메소드들이 제대로 동작하는지 테스트하고 싶을 수 있다.  
```python
# mod1.py
def sum(a,b):
    return a + b

def safe_sum(a,b):
    if type(a) != type(b):
        print('더할 수 없습니다')
        return
    else:
        result = a + b
    return result
    
# test code
print(safe_sum('1',4))
print(safe_sum(1,4))
```
테스트 결과 메소드가 제대로 동작하니 다른 모듈 내 import를 해보자.  

```python
>>> import mod1
더할 수 없습니다
None
5
>>>
```
단순히 import mod1만 했는데, mod1 내 테스트 코드들이 실행되었다.  
import는 해당 모듈을 가져올 뿐 아니라 실행까지 시킨다.  
즉, import한 모듈 내 실행 코드가 있다면 (print 등) 이 코드가 작업 파일에서도 실행된다.  
이를 해결하기 위해서는 __name__과 __main__라는 내장 변수를 활용한 조건문을 작성하면 된다.  

```python
# mod1.py
def sum(a,b):
    return a + b

def safe_sum(a,b):
    if type(a) != type(b):
        print('더할 수 없습니다')
        return
    else:
        result = a + b
    return result

# test code
if __name__ == __main__:
  print(safe_sum('1',4))
  print(safe_sum(1,4))
  
#test.py
>>> import mod1
>>> # test code 실행 X
```
mod1.py를 직접 실행하면 mod1.py 모듈의 __name__ 변수에 '__main__'라는 문자열이 들어간다.  
허나 mod1을 import한 파일에서 import mod1 코드 실행 시 __name__에는 'mod1' 문자열이 들어간다.  
결과적으로 조건문에 의해 test code는 실행되지 않는다.  
