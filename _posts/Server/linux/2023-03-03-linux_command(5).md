---
title:  "[Linux] 리눅스 명령 모음 (5) 디스크 관리" 

categories:
  - LINUX
tags:
  - [linux]

toc: true
toc_sticky: true

date: 2023-03-03
last_modified_at: 2023-03-03
---
[Linux] 리눅스 명령 모음 (5) 디스크 관리
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

## 9. 디스크 관리

### 9-1. 파일 시스템 관리

#### (a) fdisk : 디스크 파티션 확인/추가/삭제 설정
```
# fdisk [옵션] [장치명]
```

|옵션|설명|
|:---:|---|
|-l|현재 디스크 파티션 테이블 정보|
|-s|특정 파티션 크기|

- **관리 모드설정**

    |옵션|내용|
    |:---:|---|
    |a|부팅 파티션을 설정|
    |d|파티션 삭제|
    |l|설정 가능한 파티션 타입 출력|
    |m|파티션 설정 도움말 출력|
    |n|새로운 파티션 생성|
    |p|현재 설정되어 있는 파티션 정보 출력|
    |t|파티션 타입 변경|
    |q|fdisk 메뉴 빠져나가기|
    |w|작업 내용 저장|

<br>

#### (b) mkfs : 새로운 파일 시스템 생성
```
# mkfs [-t filesystem_type] [옵션] <장치명>
```

|옵션|설명|
|:---:|---|
|-t [종류]|파일 시스템의 종류 선택|
|-c|파일 시스템을 생성하기 전에 bad block 검사|
|-v|작업 상태와 결과를 자세히 출력|

<br>

#### (c) mount : 파일 시스템 마운트 명령
```
mount [-t 파일시스템 유형] [-o 옵션] [장치명] [마운트_포인트]

# CD-ROM 마운트
mount -t iso9660 /dev/cdrom [마운트_포인트]

# ISO 이미지 마운트
mount -o loop /root/CentOS6.iso [마운트_포인트]
```

|옵션|설명|
|:---:|---|
|async|마운트된 파일시스템에 비동기 입출력을 사용|
|auto|/etc/fstab에 지정된 파일시스템에 대해 부팅 시에 자동으로 마운트|
|defaults|rw, suid, dev, exec, auto, nouser, async를 종합적으로 사용|
|dev|해당 파일시스템을 문자 디바이스나 블록 디바이스를 이용해 해석|
|exec|파일 시스템에 포함된 프로그램을 실행할 수 있도록 함|
|noauto|자동 마운트가 되지 않도록 함|
|noexec|해당 파일 시스템의 프로그램이 실행되지 않도록 함, 특정 보안 목적을 위해 사용|
|nosuid|실행 파일에 존재하는 suid, sgid 비트의 기능 제한|
|nouser|루트(root) 외의 사용자가 파일 시스템을 마운트 하거나 언마운트 하는 것을 제한|
|ro|읽기 전용으로 마운트|
|rw|읽기와 쓰기 가능하도록 마운트|
|suid|실행 파일에 존재하는 suid, sgid 비트의 기능을 사용|
|sync|마운트된 파일시스템에 동기식 입출력을 사용|
|user|일반 사용자의 파일시스템 마운트 허용|
|users|모든 일반 사용자가 파일 시스템을 마운트, 언마운트 가능하도록 허용|
|noatime|acess time을 기록하지 않음, 자주 파일에 액세스 할 경우 유용|

<br>

#### (d) umount : 마운트 해제

<br>

#### (e) blkid : UUID 확인

- UUID : 네트워크에서 개체들을 식별하고 구별하기 위한 고유한 이름

<br>

#### (f) 파일 시스템 마운트 관리 파일(/etc/fstab)

- 부팅되면서 파일 시스템을 어디에 자동으로 마운트하고, 외부 장치들에 대한 마운트를 어떻게 설
정하는지, 권한 및 복구 등의 옵션을 어떻게 이용할 지 지정하는 파일

- 시스템 부팅 시 /etc/fstab에 기록되어 있는 순서대로 파티션이 마운트 되어 한 개의 디렉토리 트리가 만들
어 짐

![image](https://user-images.githubusercontent.com/42735894/222946855-ab80bbd5-792a-406c-ad49-0d903b74dfd0.png){: width="100%" height="100%"}

![eqeqwe123123123](https://user-images.githubusercontent.com/42735894/222947436-846c0305-732c-499e-8be9-058102902ce0.PNG){: width="100%" height="100%"}


<br>

### 9-2. 파일 시스템 점검

#### (a) df : 파일 시스템에 할당된 용량, 사용량, 등을 출력
```
df [옵션] 
```

|옵션|설명|
|:---:|---|
|-a|모든 파일 시스템의 정보 확인|
|-i|Size 대신 inode 사용 정보 확인|
|-m|단위를 MB로 확인|
|-t|지정한 종류의 파일 시스템 확인|
|-x|지정한 종류의 파일 시스템을 제외한 정보 확인|

<br>

#### (b) du : 파일 및 디렉터리의 용량 확인
```
du [옵션] [파일 또는 디렉터리 이름]
```

|옵션|설명|
|:---:|---|
|-a|파일까지 확인(default : 디렉터리)|
|-s|전체 용량의 합계를 확인|
|-b|단위를 byte로 확인|
|-k|단위를 KB로 확인|
|-l|하드 링크된 파일까지 확인|
|-h|용량 단위 표시|

<br>

#### (c) fsck : 파일 시스템 검사/복구 

- fask 명령은 손상된 디렉터리나 파일을 수정할 때 임시로 /lost+found 디렉터리에서 작업을 수행하고 정상적인 복구가 되면 사라진다.

|옵션|설명|
|:---:|---|
|-a|명령 수행에 대한 확인 질문 없이 무조건 수행|
|-r|사용자에게 확인 후 작업 수행|
|-A|/etc/fastb에 정의되어 있는 모든 파일 시스템 체크|
|-P|-A 옵션 사용시 루트 파일 시스템을 다른 파일 시스템과 병렬로 함께 체크|
|-v|점검 내역 상세 보기, 자세한 출력|
|-y|모든 응답을 다 yes로 해서 자동으로 실행하는 것|
|-f|파일 시스템이 이상 유무에 상관 없이 강제적으로 파일 시스템을 체크|

<br>

### 9-4. 스왑(Swap) 생성

#### (a) mkswap : 스왑 파티션이나 스왑 파일을 생성
```
mkswap [옵션] [스왑파일 [size]] or [스왑 파티션]
```

<br>

#### (b) mkswap : 스왑 파티션이나 스왑 파일을 생성
```
swapon [옵션] [스왑 파일] or [스왑 파티션]
```

<br>

#### (c) swapoff : 스왑 파티션, 파일을 비활성화
```
swapoff [옵션] [스왑 파일] or [스왑 파티션]
```

<br>

#### (d) free : 현재 사용 중인 스왑 메모리 상태 출력

<br>

### 9-5. 디스크 할당량 관리

#### (a) Disk Quota

- 사용자 및 그룹의 디스크 사용량과 생성할 수 있는 파일의 개수를 제한

#### (b) Disk Quota 설정 순서

- **/etc/fstab 설정**

    - **userquota :** 사용자 계정에 대한 용량 제한

    - **grpquota  :** 그룹에 대한 용량 제한

    ![image](https://user-images.githubusercontent.com/42735894/222947865-029564b7-8b26-40c5-b0de-b28576724fb9.png){: width="100%" height="100%"}

- **eboot 또는 remount (mount -o remount /home)**

- **Quota Database 생성**

    - 계정 및 그룹들이 현재 사용하고 있는 디스크 정보를 저장하고 있음

    - **quotacheck :** Quota 기록 파일을 가장 최근의 상태로 업데이트

    ```
    quotacheck [옵션]
    ```

    |옵션|설명|
    |:---:|---|
    |-a|디스크 사용량 할당이 활성화되고 /etc/fstab에 마운트 된 모든 파일시스템 확인|
    |-u|사용자 계정 디스크 사용량 할당 정보 체크|
    |-g|그룹 디스크 사용량 할당 정보 체크|
    |-v|사용량 할당 확인 작업의 진행을 상세한 상태 정보로 보여 줌|
    |-c|디스크 사용량 할당 파일 생성|
    |-m|파일 시스템이 동작 중인 상태에서 강제로 quotacheck를 시도|
    |-f|디스크 사용량 할당이 비활성화 시에 강제로 quotacheck를 시도|

    ![image](https://user-images.githubusercontent.com/42735894/222947974-49bd0d04-9b0c-4225-a4cc-e8f7ace9d83b.png){: width="100%" height="100%"}

- **사용자 개인 별 Quota 설정**

    - **edquota :** 사용자 계정별로 사용량을 할당하기 위한 명령

    ```
    edquota [옵션] [계정명 또는 그룹명]
    ```

    |옵션|설명|
    |:---:|---|
    |-u|사용자 디스크 할당량 설정|
    |-g|그룹 디스크 할당량 설정|
    |-t|디스크 할당량 유예기간 설정|
    |-p|디스크 할당량 설정을 다른 사용자와 동일하게 설정|

    ![image](https://user-images.githubusercontent.com/42735894/222948175-d2d86780-76e1-4f24-b01c-597f727164dc.png){: width="100%" height="100%"}

    |필드|설명|
    |:---:|---|
    |Filesystem|디스크 할당량 설정 파티션|
    |Blocks|현재 유저가 사용하고 있는 디스크 용량 (1 Block = 1024 Byte)|
    |Soft|blocks이 지정한 용량을 초과하면 경고|
    |Hard|blocks이 지정한 용량을 초과하면 쓰기 금지|
    |Inodes|현재 유저가 사용하고 있는 전체 파일 개수|
    |Soft|inodes가 지정한 파일 수를 초과하면 경고 (0은 제한 없음)|
    |Hard|inodes가 지정한 파일 수를 초과하면 쓰기 금지 (0은 제한 없음)|

- **유예 기간(Grace Period) 설정 - (edquota -t)**

    - 사용자의 계정 사용 량이 soft limit으로 지정한 용량에 도달하였을 때부터 hard limit 범위 내에서 계
정 용량을 초과하여 사용할 수 있도록 한시적으로 적용되는 기간

    - 기간이 경과되면 계정 용량은 soft limit 이상의 용량을 초과하여 사용할 수 없게 됨

    ![image](https://user-images.githubusercontent.com/42735894/222948289-e03a77a0-6eea-4fbb-b8a1-91064af2e75b.png){: width="100%" height="100%"}

- **시스템 적용(Quota 활성화)**

    - quotaon/quotaoff [파일시스템 마운트 포인트]

<br>

#### (c) requota : 파티션의 디스크 할당량 정보 출력

![image](https://user-images.githubusercontent.com/42735894/222948427-0775539b-9ea2-4af4-bd82-0722e17a4c4b.png){: width="100%" height="100%"}

<br>