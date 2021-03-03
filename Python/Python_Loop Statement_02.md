파이썬 반복문: for 문
==================
파이썬의 반복문으로는 while 문 뿐만 아니라 for 문 역시 사용 가능하다.  
다만 java의 for 문과 사뭇 다른 차이점이 존재하므로 유의하여 사용하도록 하자.  

For 문 사용(1): 기본형
--------------------
다음 예제 코드를 보면서 for문의 기본 구조를 익혀보자

```python
>>> a = [1,2,3]
>>> for k in a:
...     print(k)
... 
1
2
3
```

for문을 사용하면 in 뒤의 객체(a)의 요소(1,2,3)를 순서대로 k에 대입시킨다.  
중요한 점은 in 뒤의 객체는 무조건 **Iterable** 해야한다.  
즉, str, tuple, list 형만 들어갈 수 있다.

```python
#str을 이용한 for문 사용
>>> a = 'abc'
>>> for k in a:
...     print(k)
... 
a
b
c

#tuple을 이용한 for문 사용
>>> a = 1,2
>>> for k in a:
...     print(k)
... 
1
2

# 오류 코드: Not Iterable 한 객체를 반복할 경우
>>> a = 1
>>> for k in a:
...     print(k)
... 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not iterable
```

For 문 사용 (2): for 문 활용하기
--------------
for 문을 이용하여 단순 출력이 아닌 연산에 활용해보자.  

```python
>>> a = [(1,2),(3,4),(5,6)]
>>> for first,second in a:
...     first + second
... 
3
7
11
```

for 문 내 조건문 역시 활용할 수 있다.  
밑 코드는 5명의 학생 점수를 받고 60점 이상인 학생에게 '합격' 미만인 학생에게 '불합격'을 출력하는 프로그래밍이다.

```python
>>> score = [50, 70, 65, 40, 80]
>>> num = 0
>>> for k in score:
...     num += 1
...     if k >= 60:
...             print('%d번 학생 합격입니다.'%num)
...     else:
...             print('%d번 학생 불합격입니다.'%num)
... 
1번 학생 불합격입니다.
2번 학생 합격입니다.
3번 학생 합격입니다.
4번 학생 불합격입니다.
5번 학생 합격입니다.
```

For 문 사용 (3): range() 함수 사용하기
---------------------
파이썬의 for문은 자바 for 문과는 다르게 증감식이 포함되어 있지 않다.  
따라서 증감식을 사용하고 싶을 경우 range() 함수를 사용하면 된다.  
range() 함수의 구조는 다음과 같다:  
**range(Start Value, End Value, Step Value)**
리턴값: list  
이 때 시작값과 증감값은 디폴트 값으로 각각 0과 1이 설정되어 있다.  
즉, 생략시 0과 1이 자동으로 들어간다. 반면, 끝 값은 반드시 입력해주어야 한다.  
또한, 끝 값의 경우 마지막 값은 생략된다 즉 range(10)은 [1,2,3,4,5,6,7,8,9]를 반환한다.  

for문과 range 함수를 사용하여 1부터 100까지의 합을 구하는 프로그래밍을 작성해보자.  
```python
>>> sum = 0
>>> for i in range(1,101):
...     sum += i
... 
>>> sum
5050
```

len 함수로 range 함수를 함께 사용할 경우 List의 index로도 활용할 수 있다.
len 함수는 리스트의 길이를 반환한다. 
```python
>>> a = [1,2,3]
>>> for number in range(len(a)):
...     print(a[number])
... 
1
2
3
```

For 문 사용 (4): 내포된 for 문 사용하기
-----------
내포된 for문을 사용하면 복잡한 코드 없이 바로 실행 값을 얻을 수 있다.  
다음 예제를 보며, 내포된 for문의 편리함을 느껴보자  

**일반 for문 사용**

```python
# 기존 list 요소들에 각각 3을 곱한 새로운 list result를 반환
>>> a = [1,2,3]
>>> result = []
>>> for i in a:
...     result.append(i*3)
...
>>> result
[3, 6, 9]
```

**내포된 for문 사용**


```python
# 기존 list 요소들에 각각 3을 곱한 새로운 list result를 반환
>>> a = [1,2,3]
>>> result = [i*3 for i in a]
>>> result
[3, 6, 9]

# 기존 list 요소들 중 짝수만 반환하여 만든 새로운 list result를 
>>> a
[3, 6, 9, 12]
>>> result = [i for i in a if i % 2 ==0]
>>> result
[6, 12]
```
**주의점**
내포된 for문 사용시 ':' 은 사용하지 않는다.
