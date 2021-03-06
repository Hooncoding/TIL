네트워크 관련 명령어
===================
Summary
-------
개발자가 새로이 회사에 들어간다면 로컬 컴퓨터를 회사 네트워크에 맞게 설정해야 할지도 모른다.
오늘 배운 네트워크 관련 명령어를 익혀두면 네트워크 설정에 도움이 될 것이다. 

네트워크 설정 변경하기
---------------------
명령어를 통해 IP 주소를 변경하는 연습을 해보자.  

1.네트워크 설정을 변경하기 위해서는 네트워크 인터페이스 파일을 찾아야 한다.  
**네트워크 인터페이스 name 확인 명령어**
```
$ ifconfig
```

**네트워크 인터페이스 있는 디렉토리로 이동**
```
cd /etc/sysconfig/network-scripts/
```

**네트워크 인터페이스 수정**
```
$ vi ifcfg-ens33 -- 파일명은 다를 수 있음  

기존 dhcp(IP 자동 할당)을 static으로 변경한 이후 IP에 대한 정보를 입력해준다.  
#BOOTPROTO="dhcp" -- 기존 설정 주석 처리
------- 추가 ---------
BOOTPROTO="static"
IPADDR=192.168.0.130
NETMASK=255.255.255.0
GATEWAY=192.168.0.1
DNS=168.126.63.1
-------------------------
:wq 로 저장 후 빠져나오기
```
네트워크 설정 변경 이후 네트워크를 재시작해야 적용된다.

**네트워크 재시작**
```
systemctl restart network
```

기타 네트워크 명령어
-------------------
**네트워크 장치 시작/정지/재시작/상태확인**
```
systemctl start network
systemctl stop network
systemctl restart network
systemctl status network
```
위 명령어들은 **모든 네트워크 장치**를 대상으로 한다.

**개별 네트워크 장치 시작/정지**
```
ifup 장치이름 : 장치 시작
ifdown 장치이름 : 장치 끄기
```

**dns 서버 작동 테스트**
```
$ nslookup
```

**네트워크 상태 확인**
```
ping ip주소(or URL)
```


