# 03. Subnet Mask

## 개요

Subnet Mask는 IP Address에서 Network ID와 Host ID를 구분하기 위해 사용하는 값이다.

IP 주소만으로는 네트워크 영역과 호스트 영역을 구분할 수 없기 때문에 서브넷 마스크를 함께 사용한다.

---

## Subnet Mask란?

- Network ID와 Host ID를 구분하는 기준
- IPv4 주소와 함께 사용
- 32비트로 구성
- Network 비트는 1, Host 비트는 0으로 표현
- 동일 네트워크 여부를 판단할 때 사용

예시

```text
IP Address  : 192.168.10.100
Subnet Mask : 255.255.255.0
```

---

## 서브넷 마스크 구조

```text
255.255.255.0

11111111.11111111.11111111.00000000
```

- 1 : Network Bit
- 0 : Host Bit

따라서 위 서브넷 마스크는

```text
Network Bit : 24
Host Bit    : 8
```

를 의미한다.

---

## CIDR 표기법

CIDR(Classless Inter-Domain Routing)은 네트워크 비트 수를 간단하게 표현하는 방법이다.

```text
192.168.10.100/24
```

여기서

```text
/24
```

는 Network Bit가 24개임을 의미한다.

### 자주 사용하는 CIDR

| CIDR | Subnet Mask |
| ------ | ------ |
| /24 | 255.255.255.0 |
| /25 | 255.255.255.128 |
| /26 | 255.255.255.192 |
| /27 | 255.255.255.224 |
| /28 | 255.255.255.240 |
| /29 | 255.255.255.248 |
| /30 | 255.255.255.252 |

---

## 네트워크 주소 계산

IP Address

```text
192.168.10.100
```

Subnet Mask

```text
255.255.255.0
```

AND 연산

```text
192.168.10.100
255.255.255.0
----------------
192.168.10.0
```

결과

```text
Network Address : 192.168.10.0
```

---

## 호스트 수 계산

사용 가능한 호스트 수는 다음 공식으로 계산한다.

```text
2^(Host Bit 수) - 2
```

- Network Address 1개 제외
- Broadcast Address 1개 제외

예시

```text
192.168.10.100/24
```

Host Bit 계산

```text
32 - 24 = 8
```

사용 가능한 호스트 수

```text
2^8 - 2
= 256 - 2
= 254
```

---

## 서브넷별 호스트 수

| CIDR | Host Bit | 사용 가능한 Host |
| ------ | ------ | ------ |
| /24 | 8 | 254 |
| /25 | 7 | 126 |
| /26 | 6 | 62 |
| /27 | 5 | 30 |
| /28 | 4 | 14 |
| /29 | 3 | 6 |
| /30 | 2 | 2 |

---

## 핵심 정리

* Subnet Mask는 Network ID와 Host ID를 구분한다.
* Network Bit는 1, Host Bit는 0으로 표현된다.
* CIDR은 Network Bit 수를 나타낸다.
* Network Address는 Host Bit가 모두 0이다.
* Broadcast Address는 Host Bit가 모두 1이다.
* 사용 가능한 Host 수는 `2^(Host Bit) - 2` 공식으로 계산한다.