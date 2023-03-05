---
title:  "[가상화] 02. 하이퍼바이저의 종류" 

categories:
  - VIRTUALIZATION
tags:
  - [virtualization]

toc: true
toc_sticky: true

date: 2021-07-13
last_modified_at: 2021-07-13
---
# [가상화] 02. 하이퍼바이저의 종류
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

![Xen-kvm-반가상화-전가상화-4](https://user-images.githubusercontent.com/42735894/222968865-89c3bc0d-b49d-4b5e-b6f8-8c88d147e6ed.png){: width="100%" height="100%"}

## 🔔 Type 1 - Native or Bare-Metal Hypervisor

- **하이퍼바이저가 해당 하드웨어에 직접 설치되어 실행되는 방식**

- <u>자체적으로 관리 기능을 갖고 있지 않기에 별도의 관리 콘솔이 필요</u>하고 호스트OS가 아닌 <u>하이퍼바이저 자체에서 하드웨어를 직접 제어</u>하기 때문에 상대적으로 <u>오버헤드가 적고</u>, 물리 하드웨어의 <u>리소스 관리도 유연</u>하다.

<br>

## 🔔 Type 2 - Hosted Hypervisor

- **일반 프로그램과 같이 호스트OS에서 실행되는 소프트웨어 응용프로그램**

- 물리 하드웨어를 <u>에뮬레이트하기 때문에 오버헤드가 크며</u>, <u>게스트OS 종류에 대한 제약이 없어 거의 대부분의 OS 에서 동작시킬 수 있고, 손쉽게 도입이 가능</u>하다.

<br>

## 🔔 보호 링 계층과 하이퍼바이저

![ㅇㅁㅇㄴㅁ](https://user-images.githubusercontent.com/42735894/222968866-3980cea9-5118-45bc-829c-df93413d8ac7.png){: width="100%" height="100%"}

> 보호 링은 컴퓨터 시스템에서 계층별로 보호 권한을 구분한 구조로, 시스템 자원 접근에 대한 보안 매커니즘을 나타낸다 "Ring 0"은 시스템 커널을 의미하며 물리 리소스와 직접 상호작용하고, "Ring 3"은 사용자 모드에서는 직접적인 물리 리소스에 접근해서 할 수 있는 것이 제한적이며, "Ring 1, 2"는 장치 드라이버 레벨이다. <br><br>
Type 2의 경우, 호스트OS 위에서 하드웨어를 에뮬레이팅 함으로써 자원을 가상화하고 가상화된 자원을 가상머신에게 할당하기 때문에 하이퍼바이저는 Ring 0에 위치하고 해당 하이퍼바이저 기반의 가상머신은 Ring 1에서 동작하게 된다. <br><br>
반면 Type 1의 하이퍼바이저의 경우, 전가상화와 반가상화 하이퍼바이저 여부에 따라 링 계층에서 상중하는 위치가 달라진다.