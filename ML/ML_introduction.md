머신러닝이란 무엇인가
==
머신러닝이란 애플리케이션을 수정하지 않고도 데이터를 기반으로   
패턴을 학습하고 결과를 예측하는 알고리즘 기법이다.

머신러닝의 종류
--
머신러닝은 크게 세 가지 종류가 있다.  
  - 지도 학습
    - 회귀
    - 분류 
  - 비 지도 학습
    - 분류
    - 군집
  - 강화 학습

지도 학습이란 정해진 답을 가지고 학습 하는 학습법을 말한다.    
딥러닝도 지도 학습의 한 종류이다.  
비 지도 학습이란 정해진 답이 없이 학습하는 학습법을 말한다.  
주로 답을 만들기 위해 비 지도 학습을 한다.  

학습의 의미
-- 
머신러닝이 인류에게 제공하는 것은 '예측'이다.  
즉, 어떤 test dataset을 기계에게 던져주면  
기계가 해당 dataset이 무엇인지 예측하여 제공한다.  
이 때 정답과 예측간에는 오차가 존재한다.  
당연히 학습 초기에는 오차가 크겠지만 학습 모델이 잘 짜였다는 가정하에   
학습 빈도가 높아질 수록 오차가 줄어든다.  
바로 이 오차가 축소되는 과정을 학습이라고 한다. 

학습 과정
  1. 데이터를 준다
  2. 학습 알고리즘을 실행한다
  3. 예측 결과가 나온다
  4. 오차가 나온다 (정답 - 예측 결과)
  5. 오차를 학습 알고리즘에 반영한다 (weight 수정)
  6. 학습이 종료되면 model이 나온다
  7. new 데이터가 입력되면 Model을 거쳐 예측값이 나온다.

