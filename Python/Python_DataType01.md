파이썬의 데이터 타입
===================

파이썬의 데이터 타입은 '하나'다
------------------------------
자바에서는 정수, 실수, 문자, 참조 등 다양한 데이터 타입이 있었다.  
놀랍게도 파이썬에서는 데이터 타입이 **'참조형' 하나만 존재**한다.  
처음에는 이 말을 이해하지 못했는데 코드를 몇 줄 해보니 이 말은 꽤나 충격적이었다.  

```
>>> a = 1
>>> a
1
>>> a = 'hi'
>>> a
hi
```
자바를 배운 사람(나 포함)들이 이 코드를 보면 몇 가지 포인트에서 충격이다.  

1. 변수 앞에 데이터 타입이 없네?
2. 정수를 대입한 변수에 문자열을 대입할 수 있네?
3. ; 가 없네?

하나씩 살펴보자.

변수 앞에 데이터 타입을 정의하지 않는다.
-------------------------------------
자바에서는 변수 선언 시 반드시 데이터 타입을 입력해줘야 한다. (안할 시 에러)  
즉, a 에 1이란 값을 넣기 위해서는 a를 int로 정의한 이후 값을 대입해야 한다.  

파이썬에서는 모든 변수의 데이터 타입이 참조형이기 때문에 굳이 써주지 않는다.    
여기서 의문은 그렇다면 a는 도대체 뭘 참조하는 변수길래 1이란 Scalar를 받을 수 있을까?  

```
>>> a = 1
>>> type(a)
<class 'int'>
```

a는 int 클래스를 참조하는 변수이다.

결론적으로, 파이썬 내에는 다양한 데이터 타입(정수, 실수, 문자 등)을 받을 수 있는 클래스가 존재한다.  
특정 변수에 값을 대입할 시 그 값의 타입에 따라 컴파일 시 자동으로 변수가 참조할 class를 할당한다.  
이를 **'동적 할당'** 이라고 한다.

변수에 대입하는 값에 따라 변수가 참조하는 클래스가 변경된다
-------------------------------------------------------
정수를 대입받은 변수 a에 문자열 '123'을 대입하면 a가 참조하는 클래스가 변경된다.  
즉, a는 int Class를 참조하는 변수에서 str Class를 참조하는 변수로 변경된다.  
위 변경은 변수 초기 선언 때와 마찬가지로 컴파일 시 '동적 할당'된다.

```
>>> a = 1
>>> type(a)
<class 'int'>
>>> a = '123'
>>> type(a)
<class 'str'>
```

세미콜론은 써도되고 안써도 된다.
------------------------------
안써도 된다는 점만 유의하자. (굳이 쓸 필요가 없다.)