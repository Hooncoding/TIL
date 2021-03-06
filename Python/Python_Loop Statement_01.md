파이썬 반복문: while
===============
파이썬에서 역시 반복문(for, while)이 사용 가능하다.  
이 문서에서는 while 문을 다룬다.  
조건문과 마찬가지로 ':'과 들여쓰기 사용에 주의하자.

While 문 사용 (1): 기본형
-----------------------
열 번찍어야 넘어가는 나무가 있다고 가정하고 나무를 찍어 넘겨보자!

```python
>>> treehit = 0
>>> while treehit < 10:
...     treehit += 1
...     print('나무를 %d번 찍었습니다'%treehit)
...     if treehit == 10:
...             print('나무가 넘어갑니다')
... 
나무를 1번 찍었습니다
나무를 2번 찍었습니다
나무를 3번 찍었습니다
나무를 4번 찍었습니다
나무를 5번 찍었습니다
나무를 6번 찍었습니다
나무를 7번 찍었습니다
나무를 8번 찍었습니다
나무를 9번 찍었습니다
나무를 10번 찍었습니다
나무가 넘어갑니다
>>> 
```

While 문 사용 (2): Break 사용하기
---------------------
10 잔의 커피 재고가 있는 자판기가 있다고 가정하자.  
이 자판기는 커피 재고가 다 떨어질 때 까지 커피를 판매하고 재고가 없을 시 판매 종료를 한다.  
While 문을 통해 해당 자판기를 프로그래밍 해보자.
```python
>>> money = 1
>>> coffee = 10
>>> while money: # money가 0이 아닌 이상 무한 반복된다.
...     coffee -= 1 # 커피 갯수 1 차감
...     print('커피가 나옵니다')
...     print('남은 커피는 %d잔 입니다'%coffee) # 커피 재고 출력
...     if not coffee: # 커피 재고가 0이면
...             print('커피가 없습니다. 판매를 종료합니다.') # 문구 출력
...             break # 무한 반복문 탈출
... 
# 출력 결과
커피가 나옵니다
남은 커피는 9잔 입니다
커피가 나옵니다
남은 커피는 8잔 입니다
커피가 나옵니다
남은 커피는 7잔 입니다
커피가 나옵니다
남은 커피는 6잔 입니다
커피가 나옵니다
남은 커피는 5잔 입니다
커피가 나옵니다
남은 커피는 4잔 입니다
커피가 나옵니다
남은 커피는 3잔 입니다
커피가 나옵니다
남은 커피는 2잔 입니다
커피가 나옵니다
남은 커피는 1잔 입니다
커피가 나옵니다
남은 커피는 0잔 입니다
커피가 없습니다. 판매를 종료합니다.
```

While 문 사용 (3): 반복문 내 input, 조건문 사용하기
-------------------------------------
이번엔 자판기 투입금액을 직접 입력받고 적정 금액이 투입되면 커피를 주는 자판기 프로그래밍을 해보자

```python
>>> while True: # break 조건에 맞을 때 까지 무한 반복
...     money = int(input('금액을 투입하세요 :')) # 키보드로 부터 input 받기 (추후에 자세히 다룰 예정)
...     if money == 300:
...             print('커피가 나옵니다')
...             coffee -= 1
...     elif money > 300:
...             print('커피와 거스름돈 %d원이 나옵니다'%(money-300))
...             coffee -= 1
...     else:
...             print('투입 금액이 부족합니다')
...     if not coffee:
...             print('커피가 없습니다. 판매종료.')
...             break
... 
# 출력 결과
금액을 투입하세요 :100
투입 금액이 부족합니다
금액을 투입하세요 :300
커피가 나옵니다
금액을 투입하세요 :400
커피와 거스름돈 100원이 나옵니다
금액을 투입하세요 :300
커피가 나옵니다
커피가 없습니다. 판매종료.
>>> 

```

While 문 사용 (4): Continue 사용하기
---------------------------------
1 부터 10까지 홀수만 출력하는 프로그래밍을 한다고 가정하자.  
반복문을 써서 1 ~ 10 까지의 수 중 홀수면 print를 쨕수면 skip을 하면 된다.  
이때 continue를 사용한다.  
while 문 내 Continue 가 실행되면 continue 밑의 코드는 실행되지 않고 다시 반복문의 첫 문장부터 실행된다.  

```python
>>> a = 0
>>> while a<10:
...     a+=1
...     if(a%2 ==0):
...             continue
...     print(a)
... 
1
3
5
7
9
```

**pass/break와의 차이점**
continue, pass, break는 모두 무언가 skip한다는 용도지만, 쓰임새가 다르다.  
예제를 통해 continue/pass/break의 용도를 구별해보자  

**pass: 조건문 내 아무 실행도 하고 싶지 않을 때**
```python
>>> a = 0 
>>> while a<10:
...     a+=1
...     if a%2 ==0:
...             pass
...             print('짝수입니다')
...     print(a)
... 
1
짝수입니다
2
3
짝수입니다
4
5
짝수입니다
6
7
짝수입니다
8
9
짝수입니다
10
```
모든 문장이 출력되었다. 즉, pass는 조건에 맞더라도 아무런 실행을 원치 않을 경우 사용한다.  
즉, 반복문에 어떠한 영향도 끼치지 못한다.

**break: 반복문 강제 탈출**
```python
>>> a = 0
>>> while a<10:
...     a+=1
...     if a%2==0:
...             break
...     print(a)
... 
1
```
홀수인 1까지만 출력되고 실행이 종료 되었다.  
즉, 짝수인 2를 만났고 조건문에 걸려 break가 실행되었다.  
따라서 남은 작업을 skip하고 반복문을 강제로 종료했다.  
continue는 조건문과 함께 사용시 특정 조건의 경우만 종료 했지만 break는 반복문 자체가 종료된다.
