파일 찾기 관련 명령어
====================
Summary
--------
리눅스에서 특정 파일의 위치를 검색하는 명령어들을 배웠다.  
find, which whereis 등의 명령어가 있지만 find 정도만 알아도 된다.  

find 기본 명령어
-------------

**파일 이름으로 찾기(-name 옵션)**
```
find /home -name hong : home 디렉토리 내 hong 이름을 가진 파일 찾기
```

**소유자 명으로 찾기(-user 옵션)**
```
find /home -user user1 : home 디렉토리 내 user1의 소유인 파일 찾기
```

**생성 시점으로 찾기(-newer 옵션)**
```
find /home -newer 비교할파일 : home 디렉토리 내 비교할파일의 생성 시점 이후의 파일 찾기
find /home !-newer 비교할파일: home 디렉토리 내 비교할파일의 생성 시점 이전의 파일 찾기
```

**허가 권한으로 찾기(-perm 옵션)**
```
find /home -perm 777 : home 디렉토리 내 rwx 권한이 부여된 파일 찾기
```

**용량으로 찾기(-size 옵션)**
```
find /home -size 0k : home 디렉토리 내 용량이 0kb인 파일 찾기
```

find 응용 명령어
----------------
find 명령어는 print와 exec Action이 있다.  
디폴트는 print이며 exec 액션을 사용시 find를 더 잘 활용할 수 있다.

```
find /home -size 0k rm {}\; : home 디렉토리 내 용량이 0인 파일 삭제해라.

find /home -name *.txt ls -l {}\; : home 디렉토리 내 확장자가 txt인 파일 상세 정보 출력해라.
```
