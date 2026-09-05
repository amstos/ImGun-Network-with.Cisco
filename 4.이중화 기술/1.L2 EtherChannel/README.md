# L2 EtherChannel

## 개요
EtherChannel은 여러 개의 물리적 포트를 하나의 논리적 포트로 묶어 대역폭을 증가시키고, 링크 장애 시 자동으로 트래픽을 재분배하는 기술이다.


- 여러 개의 **이더넷 링크(포트)를 하나의 논리적 링크로 묶어** 트래픽을 분산 및 균형 조절
- **부하 분산(Load Balancing) 및 이중화(Fault Tolerance)** 제공
- **STP(Spanning Tree Protocol)에서는 하나의 링크로 인식** → 루프 방지 가능
- **VLAN 태깅(Trunk) 또는 액세스 모드(Access)로 설정 가능**
- **MAC 주소 기반 스위칭만 수행** (라우팅 불가)
- **STP(Spanning Tree Protocol)의 영향을 받음** (하지만 하나의 논리적 링크로 인식되어 루프 방지 가능)


---

## EtherChannel의 종류

### Static모드
- 설정된 포트들을 강제로 EtherChannel로 묶음
- **PAgP 또는 LACP 없이 수동으로 포트를 추가**
- 두 스위치가 모두 **On 모드**여야 정상적으로 연결

🔹 **설정 방법 (Cisco)**

```bash
Switch(config-if-range)# channel-group 1 mode on

```

### PAgP 모드
- **Cisco 독점 프로토콜**
- PAgP를 지원하는 장비끼리만 자동으로 EtherChannel을 설정
- **모드 종류**:
    - `auto`: 상대방이 `desirable`이면 EtherChannel 구성
    - `desirable`: 상대방이 `auto` 또는 `desirable`이면 EtherChannel 구성
  
🔹 **설정 방법 (Cisco)**

```bash
Switch(config-if-range)# channel-protocol pagp
Switch(config-if-range)# channel-group 1 mode auto  # 수동 대기 모드
Switch(config-if-range)# channel-group 1 mode desirable  # 적극적 협상 모드

```

### LACP 모드
- **IEEE 표준(802.3ad) 프로토콜**
- **다양한 벤더 장비 간 EtherChannel 지원 가능**
- **모드 종류**:
    - `passive`: 상대방이 `active`이면 EtherChannel 구성
    - `active`: 상대방이 `active` 또는 `passive`이면 EtherChannel 구성

🔹 **설정 방법 (Cisco)**
```bash
Switch(config-if-range)# channel-protocol lacp
Switch(config-if-range)# channel-group 1 mode passive  # 수동 대기 모드
Switch(config-if-range)# channel-group 1 mode active  # 적극적 협상 모드
```

---

## EtherChannel 부하 분산(Load Balancing) 방식
EtherChannel은 **트래픽을 분산**할 때 여러 기준을 사용할 수 있음.

| 부하 분산 기준 | 설명 |
| --- | --- |
| **src-mac** | 송신자 MAC 주소 기반 분산 |
| **dst-mac** | 수신자 MAC 주소 기반 분산 |
| **src-dst-mac** | 송신 및 수신 MAC 주소 기반 분산 |
| **src-ip** | 송신자 IP 주소 기반 분산 |
| **dst-ip** | 수신자 IP 주소 기반 분산 |
| **src-dst-ip** | 송신 및 수신 IP 주소 기반 분산 |
| **src-port** | 송신자 포트 기반 분산 |
| **dst-port** | 수신자 포트 기반 분산 |

** EtherChannel 부하 분산 설정 방법 (Cisco)**

```bash
Switch(config)# port-channel load-balance src-dst-ip

```

---


## **EtherChannel 문제 해결 (Troubleshooting)**

🔹 **EtherChannel이 활성화되지 않는 경우**

### EtherChannel 상태 확인 명령어
```bash
Switch# show etherchannel summary

```

### EtherChannel 삭제 명령어

포트의 채널 그룹 삭제
```bash
Switch(config)# interface range f0/1 - 2
Switch(config)# no channel-group 1
```

포트채널 인터페이스 자체 삭제
```bash
Switch(config)# no interface port-channel 1
```

- **(I) 상태**: 구성 오류 발생 (Configuration Issue)
- **(D) 상태**: 비활성화된 상태 (Down)

🔹 **해결 방법**

1️⃣ 두 스위치가 같은 **EtherChannel 모드(PAgP, LACP, On Mode)** 사용 여부 확인

2️⃣ 포트 속성(속도, Duplex, VLAN 설정)이 동일한지 확인

3️⃣ `show interfaces trunk` 명령어로 VLAN 트렁킹 설정 확인





















