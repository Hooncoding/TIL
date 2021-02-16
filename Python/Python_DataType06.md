파이썬 데이터 타입: Dictionary 와 Set 형
==================================
파이썬의 딕셔너리, Set 형은 각각 자바의 HashMap과 Set과 기능이나 형태가 비슷하다.  
또한, 여러개의 객체를 저장할 수 있다는 점에서 List나 Tuple과 유사하나, index가 존재하지 않는다는 차이점이 있다.  

딕셔너리형 변수 선언하기
----------------------
딕셔너리 형 변수 선언의 형태는 다음과 같다.  
변수명 = {키1:값, 키2:값, 키3:값, ...}

```python
dict = {'name':'dylan', 'phone':'01091592403', 'birth':'0727'}
```

**주의점**  
딕셔너리의 Key 자리에는 List형이 올 수 없다.  
Key 값은 변경 불가능한 값이 들어와야 하는데, List는 불가능하다.  
Tuple이나 문자열은 가능하다

딕셔너리 조회 및 변경하기
---------------------
**Key로 Value 조회**

```python
>>> dict = {'name':'dylan', 'phone':'01091592403', 'birth':'0727'}
>>> dict['name']
dylan
```

**딕셔너리 쌍 추가, 삭제**

```python
-----------
쌍 추가
-----------
>>> dict = {'name':'dylan', 'phone':'01091592403', 'birth':'0727'}
>>> dict['city'] = 'seoul'
>>> dict
{'name':'dylan', 'phone':'01091592403', 'birth':'0727', 'city':'seoul'}

-----------
쌍 삭제
-----------
>>> del dict['city']
>>> dict
{'name':'dylan', 'phone':'01091592403', 'birth':'0727'}


-----------
쌍 수정
-----------
>>> dict['name'] = '한상훈'
>>> dict
{'name':'한상훈', 'phone':'01091592403', 'birth':'0727'}
```

딕셔너리형 내장 함수
---------------

**딕셔너리의 키 값들로 리스트 만들기: keys()**
```python
>>> dict = {'name':'dylan', 'phone':'01091592403', 'birth':'0727'}
>>> b = dict.keys()
>>> b
dict_keys(['name','phone','birth'])
>>> type(b)
<class 'dict_keys'>

keys() 함수 사용시 리턴 값의 형태는 dict_keys로 정확히는 리스트가 아니다.
따라서 리턴 값을 리스트로 만들어주어야 리스트의 인덱싱 등을 이용할 수 있다.
>>> b = list(a.keys())
>>> b
['name', 'phone', 'birth']
>>> b[0]
'name'
```
