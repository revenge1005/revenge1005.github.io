---
title:  "[Linux] 리눅스 명령 모음 (6) Log" 

categories:
  - LINUX
tags:
  - [linux]

toc: true
toc_sticky: true

date: 2023-03-03
last_modified_at: 2023-03-03
---
[Linux] 리눅스 명령 모음 (6) Log
---

<style>
table {
    font-size: 12pt;
}
table th:first-of-type {
    width: 5%;
}
table th:nth-of-type(2) {
    width: 15%;
}
table th:nth-of-type(3) {
    width: 50%;
}
table th:nth-of-type(4) {
    width: 30%;
}
</style>

<br>

## 9. Log

### 9-1. 로그 파일 종류

#### (a) 현재 로그인한 사용자 상태정보 - /var/run/utmp

- binary 파일로 되어 있어 내용 확인을 위해서 **w, who, finger 등의 명령 사용**

- Linux : /var/run/utmp , Unix : /var/adm/utmpx

![eqweqweqwe](https://user-images.githubusercontent.com/42735894/222949135-15a9d53b-9e31-4b18-a130-6a3eba4d8e27.png){: width="100%" height="100%"}

<br>

#### (b) 사용자의 로그인/로그아웃 정보 - /var/log/wtmp

- **사용자의 로그인/로그아웃 정보, 시스템 Booting/Shutdown 정보에 대한 담고 있음**

- binary 파일로 되어 있어 내용 확인을 위해서 **last 명령 사용**

- Linux : /var/log/wtmp , Unix : /var/adm/wtmpx

![qeqeewq](https://user-images.githubusercontent.com/42735894/222949204-fe31ad0b-ee95-4ff0-b865-b14f5ef08ade.png){: width="100%" height="100%"}

<br>

#### (c) 최근에 로그인한 정보 - /var/log/lastlog

- binary 파일로 되어 있어 내용 확인을 위해서 **lastlog, finger 명령 사용**

- Linux : /var/log/lastlog , Unix : /var/adm/lastlog

![qeweqwesd1211](https://user-images.githubusercontent.com/42735894/222949272-b126b4ca-38ca-4f65-968c-7776642945c6.png){: width="100%" height="100%"}

<br>

#### (d) 로그인 실패한 정보 - /var/log/btmp

- binary 파일로 되어 있어 **lastb 명령으로 사용, 실패한 모든 로그를 남김**

- Linux : /var/log/btmp , Unix : /var/adm/loginlog

![qweqwe333333](https://user-images.githubusercontent.com/42735894/222949451-311459fc-0087-4589-afcf-4656b3a2c7b5.png){: width="100%" height="100%"}

<br>

#### (e) su 명령을 사용 정보 - /var/log/sulog

- Linux : /var/log/sulog , Unix : /var/adm/sulog

![addsae131321](https://user-images.githubusercontent.com/42735894/222949592-560c7d91-ccc3-4753-985c-8d76516e1142.png){: width="100%" height="100%"}

<br>

#### (f) 모든 사용자가 사용했던 명령, 터미널, 프로세스 시작 시간 등의 정보 - acct/pacct

- binary 파일로 되어 있어 내용 확인을 위해서 **lastcomm 명령 사용**

- Linux(/var/account/pacct), **기본 생성되는 로그 파일이 아니므로 【accton /var/account/pacct】 명령 실행 필요**

- Unix(/var/adm/pacct), **기본 생성되는 로그 파일이 아니므로 【/usr/lib/acct/accton /var/adm/pacct】 명령 실행 필요**

![3213ㄴㅁㅇㅁㄴㅇ](https://user-images.githubusercontent.com/42735894/222949845-89e61ff1-8f53-415a-810e-73837a36d499.png){: width="100%" height="100%"}

<br>

#### (g) 각 사용자별로 실행한 명령어 정보 - history

- 계정별 홈 디렉토리에 존재하며, “.쉘종류_history” 형식으로 생성되고 편집기를 통해 내용을 확인하거나 history 명령을 이용

<br>

#### (h) 사용자 인증에 대한 정보 - /var/log/secure

- 사용자 계정 생성/삭제, 원격 로그인 등의 사용자 인증에 대한 정보를 기록

![123123dadas](https://user-images.githubusercontent.com/42735894/222949664-d69d4f25-e4fc-4087-ae48-c9ab6617d2b7.png){: width="100%" height="100%"}

<br>

#### (i) Messages 로그 파일 - /var/log/messages

- 시스템 로그 파일로, 시스템 운영에 대한 전반적인 메시지를 저장, 주로 시스템 데몬 들의 실행상황과 내역, 사용자들의 접속 정보, TCP Wrapper 접근 제어 정보 등

![31313ㄴ](https://user-images.githubusercontent.com/42735894/222950005-48b1d4ad-071e-4763-8937-ef022df5cb1e.png){: width="100%" height="100%"}

<br>

#### (j) 부팅될 때 출력되는 모든 메시지 기록 - /var/log/dmesg, dmesg 명령

![31231231ㄴㄴ](https://user-images.githubusercontent.com/42735894/222950059-ce867bcb-bf7b-4b3b-b3be-aa10f4d25b6a.png){: width="100%" height="100%"}

<br>

### 9-2. 기타 로그 파일 종류

#### (a) 부팅 동작에서 서비스 데몬들의 실행 상태정보 기록 - /var/log/boot.log

<br>

#### (b) crond 서비스 동작에서 예약 작업의 동작 상태 정보 - /var/log/cron

<br>

#### (c) 웹서버 접속, 오류 기록 - /var/log/httpd/access_log, /var/log/httpd/error.log

<br>

#### (d) 부팅될 때 출력되는 모든 메시지 기록 - /var/log/dmesg

<br>

#### (e) 메일 서버의 동작 상태 정보 - /var/log/maillog

<br>

#### (f) 네임서버의 로그 - /var/log/named.log

<br>

#### (g) FTP 로그 - /var/log/xferlog

![weqe123131](https://user-images.githubusercontent.com/42735894/222950204-8265d890-3b1e-4ec5-abef-7756a543335a.png){: width="100%" height="100%"}

![eqwee21313](https://user-images.githubusercontent.com/42735894/222950226-d4ad0369-0663-4a85-9acf-be56966d1c0d.png){: width="100%" height="100%"}

<br>

---

<br>

## 10. 시스템 로그 분석 및 관리

### 10-1. 시스템 로그 분석 - rsyslog

- 로그를 기록하는 데몬 프로세스로 rsyslogd 라는 프로그램에 의해 로그를 기록

- rsyslogd의 설정 파일인 /etc/syslogd.conf 파일을 읽어서 로그를 기록할 수준을 결정

![qewewq21312312331](https://user-images.githubusercontent.com/42735894/222950339-21df4dfe-c4c1-42b2-a6bc-6a8d90267c2b.png){: width="100%" height="100%"}

![weq2313123](https://user-images.githubusercontent.com/42735894/222950369-7f37dc71-dd8f-4e03-923b-03db7037f0bb.png){: width="100%" height="100%"}

```
# 커널에 관련된 로그를 /dev/console에 출력하라는 의미
ker.*	/dev/console


# 모든 서비스에 대한 info 수준의 이상의 로그를 /var/log/messages로 기록
# mail, authpriv, cron 서비스는 로그를 /var/log/messages 로그에 기록 안함
*.info;mail.none;authpriv.none;cron.none	/var/log/messages

# authpriv에 속하는 서비스(xinetd, telnet, ftp, finger 등)의 
# 모든 로그 수준의 로그 수준의 로그(*)를 /var/log/secure 로그 파일에 기록하라는 의미
authpriv.*	/var/log/secure
 
# 메일 서비스에 관련된 모든 로그 수준의 로그(*)를 /var/log/maillog에 기록
mail.*	/var/log/maillog


# crond 데몬과 atd 데몬 등에 의해 발생되는 모든 로그 수준의 로그(*)를 /var/log/cron 로그 파일에 기록하라는 의미
cron.*	/var/log/cron

# 모든 서비스(*)의 emerg 수준 이상의 로그를 모든 사용자(*)에게 보내라는 의미
*.emerg	*


# uucp, news 서비스 관련 서버의 crit 수준 이상의 로그를 /var/log/spooler에 기록
uucp,news.crit	/var/log/spooler


# 시스템이 부팅될 때의 모든 로그 수준의 로그(*)를 /var/log/boot.log에 기록
local7.*		/var/log/boot.log
```

<br>

### 10-2. 로그파일 순환 관리 - logratate

![ㄷㅂㅈㄷ2313ㄴㅇㄴ](https://user-images.githubusercontent.com/42735894/222950666-8b6618bc-e20a-487b-a1b7-52a92d399be3.png){: width="100%" height="100%"}

![ㄷㅂㅈㄷ231313ㅇㅁㅇㅁㄴㅇ](https://user-images.githubusercontent.com/42735894/222950667-1ec40ea9-0c71-44ab-9325-5f4ec078c9ae.png){: width="100%" height="100%"}

![3131321ㅈㄷㅈㄷㅂㄷㅂㅈㄷㅂㅈ](https://user-images.githubusercontent.com/42735894/222950671-fac3e57b-13f6-4102-a633-4bb954b2d752.png){: width="100%" height="100%"}

<br>