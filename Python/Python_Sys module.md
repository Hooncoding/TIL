Sys 모듈 사용하여 명령행 인자 받기
====
파이썬에서는 sys 모듈을 이용하여 명령 프롬프트에 입력한 인자를 직접 받을 수 있다.

```python
#sys1.py
# 두개 값을 입력 받아 더하기
import sys

firstnum = int(sys.argv[1])
secondnum = int(sys.argv[2])
firstnum + secondnum

--------- 명령 프롬프트 ------------
hansanghun-ui-MacBookPro:Python dylanhan$ python sys1.py 10 20
30
```

주의점1. argv의 0번 인덱스에는 파이썬 실행파일 경로가 담겨있기 때문에 입력인자는 index 1부터 입력된다.  
주의점2. sys.argv는 str을 리턴하므로, 연산을 위해서는 int로의 형변환이 필요하다.  
