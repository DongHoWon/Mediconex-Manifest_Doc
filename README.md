# 외부 시현용 자료 정리
## 필요한 자료 목록

### 1. Cygwin.zip
>1) cygtdsodbc.zip(Cygwin ODBC를 사용하기위한 .dll 파일)
>2) redis-3.2.11.tgz(redis 사용하기 위한 파일)
>3) unixODBC-2.3.6.tar(ODBC를 사용하기 위한 파일)
>4) setup-x86_64.exe(Cygwin 설치하기 위한 설치파일)
>5) TIB_rv_8.4.2_win_x86_64_vc8.zip(RVD 프로토콜 사용하기 위한 설치 파일)
>6) tibrv.tkt(RVD 프로토콜 라이센스 파일)
>7) http%3a%2f%2fftp.yz.yamagata-u.ac.jp%2fpub%2fcygwin%2f(Cygwin 백업 로컬파일 <-설치 시 이 디렉토리를 참고 해야 함.)
>8) MS-SQL DB Import

### 2. tool.zip
>1) BANDIZIP-SETUP-ONLINE.EXE
>2) Composer-Setup.exe(PHP용 패키지 관리 프로그램)
>3) Git-2.25.0-64-bit.exe
>4) TortoiseGit-2.9.0.0-64bit.msi
>5) HeidiSQL_10.1.0.5464_Setup.exe(MS-SQL 접속용 프로그램)
>5) VSCodeUserSetup-x64-1.43.0.exe
>7) xampp-windows-x64-7.4.3-0-VC15-installer.exe

### 3. SQLEXPRWT_x64_KOR.zip
>1) SQL SERVER 2012(MS-SQL 받기 위한 파일)

### 4. Middleware.zip
>1) 해당 미들웨어 파일은 종종 바뀔수 있으니 담당자에게 문의해서 받아야 함.

### 5. Laravel Webproject
>1) Github에 있는 해당 프로젝트 파일
>2) db import

* * *
## * Cygwin 설치

#### 1. Cywin폴더의 setup-x86_64.exe  프로그램을 수행한다.
<img src="https://user-images.githubusercontent.com/30614857/83103945-b48eab00-a0f2-11ea-8aa7-c02b579c0cbb.png" width="50%"></img>

#### 2. 기존 백업되어 있는 Cygwin directory를 사용할 것이므로 Install from Local Directory를 선택한다.
<img src="https://user-images.githubusercontent.com/30614857/83104390-9aa19800-a0f3-11ea-9577-5bd5b7e5e14c.png" width="50%"></img>

#### 3. Cygwin을 설치할 Root Directory를 선택한다.
<img src="https://user-images.githubusercontent.com/30614857/83104528-e3f1e780-a0f3-11ea-9c25-b6d6d115b5a1.png" width="50%"></img>

#### 4. 백업되어있는 Local Cygwin directory를 선택한다.
<img src="https://user-images.githubusercontent.com/30614857/83104596-084dc400-a0f4-11ea-8ae2-400f1a13cb65.png" width="50%"></img>

#### 5. 아래는 Cygwin, Middleware, Smart Watch와 통신하기 위한 패키지들이며 검색 후 버전을 선택해준다. 
####    추후 필요한 패키지는 추가적으로 설치할 수 있다.
  > **gcc-core 7.4.0.-1**
  
  > **cygrunsrv 1.62-1**
  
  > **openssh 7.9p1-1**
  
  > **openssl-devel 1.0.2p-1**
  
  > > ->**백업되어있는 Cygwin.exe설치 파일은 2.895 버전 기준이며openssl-devel 패키지를 설치하여야 되고 현재 Cygwin 홈페이지에있는 Cygwin.exe 2.897버전 또는 그 이상의 버전 실행파일로 Cygwin을 설치할경우 openssl-devel 패키지 대신 libssl-devel 패키지를 설치하여야 함.
(동일한 기능을 하는 패키지 이며, 2.897버전에서는 openssl-devel을 지원하지 않음.)**

  > **libiconv-devel 1.14-3**
  
  > **libiodbc-devel 3.52.8-2**
  
  > **make 4.2.1-2**
  
  > **odbc-tds 1.00.37-1**
  
  > **libcurl-devel 7.65.0-1**

  > **libcurl 7.66.0-1**

* * *


## * ODBC 드라이버 설치 및 설정

#### 1. 백업된 unixODBC-2.3.6파일을 준비한다.

#### 2. Cygwin Terminal을 Pop-Up 한다.

#### 3. cd /home수행한다.

#### 4.	mkdir install_etc 수행한다.

#### 5.	cd  install_etc를  수행한다.

#### 6. 백업된 unixODBC-2.3.6 파일을 /home/install_etc에 복사한다.

#### 7.	tar -xvf  unixODBC-2.3.6.tar 수행한다.

#### 8.	cd unixODBC-2.3.6 을 수행한다.

#### 9.	./configure을 수행 한다.

#### 10. make를 수행한다.

#### 11. Make install을 수행한다.

#### 12. 컴파일이 끝나면 드라이버 설치가 완료 된다.

#### 13. Cygwin Terminal 을 Pop-Up 한다.

#### 14. cd  /etc  수행한다.

#### 15. vi odbc.ini 입력 후 아래의 내용을 추가한다.
```
[MESDB1]
Driver=MSServer
Description=My Sample ODBC
Trace=Yes
Server=설치되어있는 IP ADDRESS
Port=1433
Database=DB NAME

[MESDB2]
Driver=MSServer
Description=My Sample ODBC
Trace=Yes
Server=설치되어있는 IP ADDRESS
Port=1433
Database=DB NAME
```
#### 16. vi odbcinst.ini 입력 후 아래의 내용을 추가한다.
```
[MSServer]
Description=Microsoft ODBC SQL Server
Driver=/usr/lib/cygtdsodbc.dll
UsageCount=1
```

#### 17. cd /usr/local/etc  수행한다.

#### 18. cp  /etc/odbc*.ini  ./  수행한다.

#### 19. 백업된 cygtdsodbc.dll 파일을 /lib 디렉토리 내 복사한다.

#### 20. 백업된 cygtdsodbc.dll 파일을 /usr/lib 디렉토리 내 복사한다.

* * *


## * REDIS 설치

#### 1. 백업된 redis-3.2.11.tgz 파일을 준비한다.

#### 2. Cygwin Terminal을 Pop-Up 한다.

#### 3. cd /home/install_etc수행한다.

#### 4. 백업된 redis-3.2.11.tgz 파일을 /home/install_etc에 복사한다.

#### 5.	tar -xvf  redis-3.2.11.tgz 수행한다.

#### 6.	cd redis-3.2.11/deps/hiredis 수행한다.

#### 7.	fmacros.h(deps/hiredis/fmacros.h) 파일에 아래 코드를 추가한다.
```
#if defined(__CYGWIN__)
#define _GNU_SOURCE
#define _DEFAULT_SOURCE
#endif
```

#### 8. net.c(deps/hiredis/net.c) 파일에 아래 내용을 추가한다.
```
#ifdef __CYGWIN__
#define TCP_KEEPCNT 8
#define TCP_KEEPINTVL 150
#define TCP_KEEPIDLE 14400
#endif
```

#### 9. /home/install_etc/redis-3.2.11/deps 디렉토리에서 make distclean을 수행한다.

#### 10. dist clean 완료 후 /deps 디렉토리에서 make hiredis linenoise lua 를 수행한다.

#### 11. cd /home/install_etc/redis-3.2.11로 디렉토리 변경 후 make를 수행한다.

#### 12. make install 를 수행한다.

#### 13. 서비스 등록을 하기 위해 관리자 권한에서 Cygwin을 Pop-up후 아래 명령어를 수행한다.
#### (경로는 자신이 설치한 드라이버에 위치하여야함)
```
cygrunsrv --install redis-server --path  /cygdrive/d/cygwin64/usr/local/bin/redis-server
```

#### 14. cygwin을 실행시킨 후 redis-server을 수행한다.

#### 15. 또다른 Cygwin pop-up창을 실행시킨 후 redis-cli를 수행한 후 PING을 입력했을 때 PONG으로 응답이 온다면 설치가 완료 됨.

* * *


## * tibco rvd 설치

#### 1. 백업된 TIBCOUniversalInstaller-x86-64.exe 파일을 실행 후 다음을 눌러서 설치해준다.

#### 2. 백업된 tibrv.tkt 파일을 C:\tibco\tibrv\8.4\bin 으로 Copy 한다.

#### 3. 윈도 프롬프트 창에서 cd C:\tivco\tibrv\8.4/bin  수행한다.

#### 4.	rvd 명령을 수행한다. 아래와 같은 메시지가 출력되면 정상 tibrv 데몬이 동작하는 것이다.
```
C:\tibco\tibrv\8.4\bin>rvd

TIB/Rendezvous daemon
Copyright 1994-2014 by TIBCO Software Inc.
All rights reserved.

Version 8.4.2 V5 2/11/2014
2018-06-29 11:50:32 rvd: Command line:
2018-06-29 11:50:32 rvd: Hostname: DESKTOP-OOOUK97
2018-06-29 11:50:32 rvd: Hostname IP address: 172.23.51.211
2018-06-29 11:50:32 rvd: Detected IP interface: 192.168.0.33 (IP00)
2018-06-29 11:50:32 rvd: Detected IP interface: 192.168.56.1 (IP01)
2018-06-29 11:50:32 rvd: Detected IP interface: 172.23.51.211 (IP02)
2018-06-29 11:50:32 rvd: Detected IP interface: 127.0.0.1 (loopback)
2018-06-29 11:50:32 rvd: Using ticket file C:\tibco\tibrv\8.4\bin\tibrv.tkt
2018-06-29 11:50:32 rvd: Http interface - http://DESKTOP-OOOUK97:7580/
```

* * *


## * WebServer 

#### 1. 백업된 XAMPP를 설치한다.

#### 2. DB password, httpd.conf 에서 root directory 설정.

#### 3. laravel project 진입 후 아래 명령어 수행.
```
composer update
php artisan key:generate
php artisan migrate

```

* * *

## * MS-SQL 설치 

#### 1. 백업된 MS-SQL설치 파일을 실행한다.

   > 1) 설치 : <http://blog.naver.com/PostView.nhn?blogId=matoker&logNo=220005679622&categoryNo=21&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView
>
   > 2) 계정생성 : <https://server-talk.tistory.com/248>
   > 3) 원격접속 : <https://server-talk.tistory.com/251>




