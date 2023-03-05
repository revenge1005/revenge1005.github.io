---
title:  "[Kickstart] PXE / Kickstart 이란?" 

categories:
  - kickstart
tags:
  - [kickstart]

toc: true
toc_sticky: true

date: 2021-07-13
last_modified_at: 2021-07-13
---
# [Kickstart] PXE / Kickstart 이란?
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


## 🔔 개념

### 1. PXE (Preboot Execution Environment)

- 네트워크 인터페이스를 이용해서 컴퓨터를 부팅할 수 있게 만들어주는 환경

- 운영체제 설치가 힘든 환경 또는 HDD, USB 등과 같은 저장매체에 구애 받지 않고 PC를 사용 위해 사용

​- PC 자체 OS로 시스템 부팅하는 것이 아니라 서버로부터 IP 할당과 부팅 이미지를 다운받아 부팅된다.

<br>

### 2. Kickstart

- RedHat Linux에서 OS 설치시 지역/시간, 사용자 패스워드 등의 환경설정 관련 내용을 파일에 담아놓으면 개별 PC에서 설치하는 동안 해당 파일을 읽어들여 설치를 자동화할 수 있도록하는 지원하는 기능

<br>

### 3. PXE 환경 구성 요소

|구성요소|설명|
|:---:|---|
|DHCP|클라이언트로부터 네트워크 정보를 할당|
|TFTP|OS 설치에 필요한 서버 구성 내용과 PXE boot 이미지 전달|
|FTP/HTTP/NFS/SAMBA|PXE 부트 이후 OS 설치에 필요한 파일 전달|
|Kickstart|OS 설치 시 환경에 대해서 미리 설정하면 해당 설정파일을 참조해서 OS 설치함|

![image](https://user-images.githubusercontent.com/42735894/222965530-a590edb8-b77e-41a2-a23e-03fb859da87d.png){: width="100%" height="100%"}

<br>

### 4. PXE 동작 과정

![weqeqweqwe](https://user-images.githubusercontent.com/42735894/222965686-97f01cad-7fcd-4bee-b434-02d30090c280.PNG){: width="100%" height="100%"}

|구성요소|설명|
|:---:|---|
|①|클라이언트가 부팅되면서 DHCP Discover 패킷을 브로드캐스트하며, 이때 패킷의 DHCP Payload에 PXE Client Flag를 넣어서 보냅니다.|
|②|서버는 Offer 패킷으로 응답하며, 클라이언트가 가져갈 IP 정보를 제공하며, 이때 DHCP에 설정된 Next-Server IP (TFTP 서버) 정보도 함께 제공됩니다.|
|③|클라이언트는 서버로 부터 받은 정보를 가지고 Request 합니다.|
|④|서버는 ACK 패킷을 통해서 최종적으로 IP 정보와 TFTP 서버 정보를 함께 보냅니다.|

![weqeqweqw2e](https://user-images.githubusercontent.com/42735894/222965690-25f21905-e050-4e0b-9ea5-7dc127b5d709.PNG){: width="100%" height="100%"}

|구성요소|설명|
|:---:|---|
|⑤ ~ ⑥|클라이언트는 TFTP 서버 정보를 통해 Network Boot Program으로 PXE 요청을 서버 에게 전송하고, 서버는 부트 로더 파일(pxelinux.0)을  잔달하고 로딩합니다.|
|⑦ ~ ⑧|클라이언트는 구성 정보를 서버에 요청하고, 서버는 PXE 부트 이미지와 기타 구성 정보가 포함된 pxelinux.cfg를 클라언트에게 전송합니다.|
|⑨ ~ ⑩|클라이언트가 pxelinux.cfg 포함된 커널과 PXE 이미지를 요청하면, 서버는 PXE 커널, 부트 이미지를 클라이언트에게  로딩합니다.|
|⑪|클라이언트는 OS 이미지 로딩을 부팅을 시작, 이때 kickstart 파일을 참고해 설치합니다|