Cron 과 At
==========
Summary
-------
Cron과 At은 특정 시점에 특정 행동을 반복적으로 수행해주는 데몬이다.
데몬이란 백그라운드 프로세스를 의미하며 윈도우의 서비스와 매칭된다.
둘의 차이점은 Cron은 주기적이고, At은 일회성 (한 번 실행되면 소멸)이다.

Cron 설정하기
------------
Cron 설정은 crontab 파일을 통해 가능하다  
crontab 파일의 위치는 다음과 같다 => etc/crontab  
crontab 설정 양식은 다음과 같다.  

>분 시 일 월 요일 유저 실행명령어 파일명

cron 관련 명령어
----------------
백문이 불여일견이다 코딩 한 번 해보자
**cron 등록하기**
```
# cd /etc //etc 디렉토리로 가기

# crontab -e //crontab 수정하기
# 00 00 1 * * root -x /home/test.txt
실행모드: /wq

=> 매월 1일 00시 00분마다 루트 유저의 home 디렉토리에 있는 text.txt 파일을 실행해라 (*은 모든을 의미)
```

**cron 확인하기**
```
# cd /etc
# crontab -l
```
현재 작동중인 cron들을 볼 수 있다.

**cron 삭제하기**
```
# cd /etc
# crontab -r
```
