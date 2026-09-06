# L3 EtherChannel

## 개요
EtherChannel은 L2와 L3 두 가지 방식으로 구현할 수 있다.

| 구분 | **L2 EtherChannel** | **L3 EtherChannel** |
| --- | --- | --- |
| **동작 계층** | **레이어 2 (L2, 데이터링크 계층)** | **레이어 3 (L3, 네트워크 계층)** |
| **포트 설정** | **Switchport 모드 (Access/Trunk) 설정 필요** | **라우팅이 필요하므로 Switchport 설정 불가** |
| **VLAN 지원 여부** | VLAN 지원 (Access, Trunk 모드 가능) | VLAN 미지원 |
| **라우팅 지원 여부** | L2 스위칭만 가능, 직접적인 라우팅 불가 | IP 주소 할당 후 직접 라우팅 가능 |
| **STP 영향** | STP가 EtherChannel을 **하나의 논리 포트**로 인식하여 루프 방지 가능 | STP 영향을 받지 않음 (L3에서 동작) |
| **IP 주소 할당** | IP 주소 할당 불가 (L2 장비이므로 MAC 기반 스위칭) | 포트 채널 인터페이스에 **IP 주소 할당 가능** |
| **라우팅 프로토콜** | 라우팅 미지원 (L2 스위칭만 수행) | OSPF, EIGRP, BGP 같은 **라우팅 프로토콜 사용 가능** |
| **사용 환경** | 일반적인 L2 스위치에서 사용 (액세스/트렁크 포트) | L3 스위치 또는 라우터에서 사용 |
| **사용 예시** | L2 스위치 간 VLAN 트래픽 전송 | L3 스위치 간 라우팅 트래픽 전송 |

## L3 EtherChannel
- **레이어 3에서 동작하는 EtherChannel**
- **각 스위치에 IP 주소를 할당하여 라우팅 수행 가능**
- **라우팅 프로토콜(OSPF, EIGRP, BGP 등)과 함께 사용 가능**
- **STP 영향을 받지 않음** (L3에서 동작하기 때문)

## Router
null

## L3 Switch
L3 스위치는 일반적인 라우터와 다르게 설정해야 한다.<BR>
Cisco 라우터의 EtherChannel은 Port-channel을 VLAN trunk처럼 사용하고 그 위에 여러 VLAN 서브인터페이스를 구성하는 방식이 지원하지 않는다.<br>
따라서 L3스위치로 이중화방식이 추천된다.

### 이더채널 구성 예시
```bash
-- L3SW --
Switch(config)# interface range f0/23 - 24
Switch(config-if-range)# channel-protocol pagp  #Static, LACP 사용 가능
Switch(config-if-range)# channel-group 1 mode desi
Switch(config-if-range)# switchport trunk encapsulation dot1q #Trunk를 사용할 경우 VLAN 태깅 방식은 802.1Q를 사용 기본은 auto
Switch(config-if-range)# switchport mode trunk 
```
### L3스위치 VLAN간 라우팅
```bash
-- L3SW --
Switch(config)# vlan 10
Switch(config)# interface vlan 10
Switch(config-if)# ip address [vlan 10 gateway] [subnet-mask]
Switch(config)# vlan 20
Switch(config)# interface vlan 20
Switch(config-if)# ip address [vlan 20 gateway] [subnet-mask]
Switch(config)# ip routing
```

---
