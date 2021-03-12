파이썬 패키지
===
패키지란 관련된 모듈들을 모아놓은 파일이다.  
여기서 관련된 모듈들이란 상호간에 유용한 기능등이 존재하여  
import가 빈번하게 일어날 경우를 말한다.  
module 관련 학습에서 서로 다른 디렉토리나 패키지에 있을 경우 import 할 때 불편했다.  
그래서 패키지에 관련 모듈을 모아놓는 것이다.  
게임을 예로 들어보자 게임은 소리, 그래픽, 모션등의 구성요소가 존재한다.  
또한 각 구성 요소마다 특정 기능을 구현하는 모듈이 따로 있을 것이다. (소리 요소 내 새 소리, 바람 소리 등)  
이때 소리와 관련된 모듈들은 소리 패키지에, 그래픽 관련 모듈들은 그래픽 패키지에 담아 분류하는 것이 좋을 것이다.  

패키지 내 존재하는 모듈 import하기
---
```python
# render.py
# 패키지 내 모듈 임포트 하기

import game.sound.echo
>>>game.sound.echo.echo_sound()
echo

#alias 부여하기
import game.sound.echo as ec
>>>ec.echo_sound()
echo

#from 사용하기: 목적: game/sound/echo.py 임포트하기
from game.sound import echo
>>> echo.echo_test()
echo

# echo.py 내 메소드중 echo_test()만 가져오기
from game.sound.echo import echo_test()
>>> echo_test()
echo

#주의: import 뒤 객체는 패키지가 올 수 없다.
import game
>>> game.sound.echo.echo_sound()
에러!!!

#컴퓨터 입장에서 game.py이라는 단일 파일 임포트 한 것으로 인식 game.py 모듈 내 sound라는 속성 없음
#결론 import 단의 끝은 결국 모듈이어야 함

#sound 패키지 내 모든 파일 import하기
from game.sound import *
>>> echo.echo_test()
echo
>>> wav.wav_test()
wav
```
