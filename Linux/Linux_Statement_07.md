PIPELINE, FILTER, REDIRECTION
=============================
Summary
-------
리눅스 내 파일 잘 활용하기 위해서는 파일을 연결하고, 정제하고, 방향을 지정해줘야 한다.
해당 역할을 수행하는 것이 각각 Pipeline, Filter, Redirection 명령어이다.

- Pipeline: 두 명령어 혹은 프로그램(파일)을 연결시키는 명령어  
- Filter: 필요한 파일만 걸러서 찾아주는 명령어
- Redirection: 표준 입출력의 방향을 바꿔주는 명령어

PIPELINE 관련 명령어
------------------- 
두 명령어나 프로그램을 연결하고 싶으면 | 명령어를 쓰면 된다.
**|을 활용한 파일 조회 예시**
```
/etc ls -l | more : /etc 디렉토리 내 모든 파일을 페이지 단위로 끊어서(more) 보겠다.
```

단순 상세 조회(ls -1) 기능에 페이지 단위로 끊어서 조회(more) 기능을 연결한 것이다.

FILTER 관련 명령어
-----------------
Filter 명령어는 다양한데, 그 중 grep을 가장 많이 쓴다.

**grep 명령어를 사용하여 특정 조건으로 출력하기 예시**

```
grep a* test.txt : text.txt 내 a로 시작하는 라인 가져오기

# 응용: Pipeline과 함께 사용하기

/etc ls | grep sys : etc 디렉토리 내 sys 문자가 들어간 프로그램 목록 출력
```

REDIRECTION 관련 명령어
======================

**Redirection 활용한 목록 저장**
```
/etc ls -l > list.txt : etc 디렉토리 내 정보들을 list.txt 파일에 저장 (기존 파일 있으면 덮어쓰기)

/etc ls -l >> list.txt : etc 디렉토리 내 정보들을 list.txt 파일에 저장 (기존 파일 있으면 이어쓰기

sort < list.txt : list.txt를 정렬해서 모니터에 출력

sort < list.txt > out.txt: list.txt를 정렬하여 out.txt에 저장
```
