파이썬 조건문: if
===========
당연하게도 여느 프로그래밍 언어처럼 파이썬에도 조건문이 존재한다.  
다만 조건문의 시작과 끝을 의미하는 {}가 존재하지 않고 ':'을 사용하며  
들여쓰기를 주의하여 사용해야 한다는 점을 유의하자.  

조건문 사용하기 (1): 에러 코드와 맞는 코드
--------------
money가 0이 아니라면 '택시를 타라'라는 문구를 출력하는 프로그래밍을 해보자  

**에러코드: 들여쓰기 미사용**
```python
>>> money = 1
>>> if money > 0:
... print('택시를 타세요')
  File "<stdin>", line 2
    print('택시를 타세요')
        ^
IndentationError: expected an indented block
```
**정상 코드**
```python
>>> if money > 0:
...     print('택시를 타세요')
... 
택시를 타세요 # 출력 결과
```

조건문 사용하기 (2): else 사용
------------------------
money가 0이 아니라면 '택시를 타라', 0이면 '걸어가라' 문구를 출력해보자.

 ```python
 >>> money = 0
>>> if money > 0:
...     print('택시를 타라')
... else:
...     print('걸어가라')
... 
걸어가라 # 출력 결과
 ```

조건문 사용하기 (3): in과 pass 사용
------------------------------
pocket 리스트 내에 'money' 요소가 있을 경우 실행 경과를 skip하고  
그렇지 않으면 '걸어가라' 문구를 출력 해보자.  

```python
>>> pocket = ['key', 'money']
>>> if 'money' in pocket:
...     pass
... else:
...     print('걸어가라')
... 
>>> # 실행 결과 없음 (money가 pocket 리스트 내 존재함)
```
조건문 사용하기 (3): elif 사용
-------------------------
elif를 사용하면 복잡한 조건문을 간단하게 사용할 수 있다. (자바의 else if와 같은 기능)

```python
>>> pocket
['cellphone', 'key']
>>> if 'money' in pocket:
...     print('현금 내고 택시를 타세요')
... elif 'card' in pocket:
...     print('카드 내고 택시를 타세요')
... else:
...     print('걸어가세요')
... 
걸어가세요 # 출력 결과
```

참고: 조건문 한 줄로 사용하기
-----------------------
들여쓰기를 사용하지 않고 if문을 한 줄로 사용할 수도 있다.  
그러나, 가독성을 위해 웬만하면 사용하지 말자.  

```python
>>> pocket
['cellphone', 'key']
>>> if 'money' in pocket:print('택시 타세요')
... else:print('걸어 가세요')
... 
걸어 가세요 # 출력 결과
```
