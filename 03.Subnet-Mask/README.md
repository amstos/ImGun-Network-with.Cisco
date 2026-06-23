# 03. Subnet Mask

## 개요

Subnet Mask는 IP Address에서 Network ID와 Host ID를 구분하기 위해 사용하는 값이다.

IP 주소만으로는 네트워크 영역과 호스트 영역을 구분할 수 없기 때문에 서브넷 마스크를 함께 사용한다.

---

# Subnet Mask란?

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

# 서브넷 마스크 구조

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

을 의미한다.

---

# CIDR 표기법

CIDR(Classless Inter-Domain Routing)은 네트워크 비트 수를 간단하게 표현하는 방법이다.

예시

```text
192.168.10.100/24
```

여기서

```text
/24
```

는 Network Bit가 24개임을 의미한다.

## 자주 사용하는 CIDR

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

# 네트워크 주소 계산

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

# Broadcast Address

Broadcast Address는 해당 네트워크에서 모든 Host에게 데이터를 전달하기 위한 주소이다.

Host Bit를 모두 1로 설정한다.

예시

```text
Network Address

192.168.10.0/24
```

Host Bit

```text
00000000
```

Broadcast

```text
11111111
```

결과

```text
Broadcast Address : 192.168.10.255
```

---

# 호스트 수 계산

사용 가능한 Host 수는 다음 공식으로 계산한다.

```text
2^(Host Bit 수) - 2
```

제외 항목

- Network Address 1개
- Broadcast Address 1개

예시

```text
192.168.10.100/24
```

Host Bit 계산

```text
32 - 24 = 8
```

사용 가능한 Host 수

```text
2^8 - 2

= 256 - 2

= 254
```

---

# 서브넷별 호스트 수

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

# VLSM (Variable Length Subnet Mask)

## 개요

VLSM(Variable Length Subnet Mask)은 하나의 네트워크를 여러 개의 서로 다른 크기의 Subnet으로 나누는 방법이다.

기존 FLSM(Fixed Length Subnet Mask)은 모든 Subnet이 같은 크기를 사용하지만,

VLSM은 필요한 Host 수에 따라 서로 다른 Subnet Mask를 사용하여 IP 주소를 효율적으로 관리한다.

---

# VLSM을 사용하는 이유

예시

하나의 네트워크

```text
192.168.10.0/24
```

필요한 네트워크

| Network | 필요한 Host |
| ------ | ------ |
| A | 100 |
| B | 50 |
| C | 20 |

---

# FLSM 방식

FLSM은 모든 네트워크를 동일한 크기로 나눈다.

가장 많은 Host가 필요한 기준으로 계산

```text
100 Host 필요
```

계산

```text
2^7 - 2 = 126
```

따라서

```text
/25 사용
```

결과

| Network | Subnet |
| ------ | ------ |
| A | 192.168.10.0/25 |
| B | 192.168.10.128/25 |
| C | 192.168.11.0/25 |

문제점

- 작은 네트워크도 큰 Subnet 사용
- IP 주소 낭비 발생

---

# VLSM 방식

필요한 Host 수에 맞춰 Subnet 크기를 다르게 할당한다.

## 1. Host 수 정렬

큰 네트워크부터 할당한다.

```text
A : 100 Host
B : 50 Host
C : 20 Host
```

---

## 2. Subnet 계산


## A Network

필요 Host

```text
100 Host
```

계산

```text
2^7 - 2 = 126
```

Subnet

```text
/25
```

할당

```text
192.168.10.0/25
```

---

## B Network

필요 Host

```text
50 Host
```

계산

```text
2^6 - 2 = 62
```

Subnet

```text
/26
```

할당

```text
192.168.10.128/26
```

---

## C Network

필요 Host

```text
20 Host
```

계산

```text
2^5 - 2 = 30
```

Subnet

```text
/27
```

할당

```text
192.168.10.192/27
```

---

# VLSM 결과

기존 네트워크

```text
192.168.10.0/24
```

결과

| Network | CIDR | Host 범위 | Broadcast |
| ------ | ------ | ------ | ------ |
| A | 192.168.10.0/25 | 192.168.10.1 ~ 126 | 192.168.10.127 |
| B | 192.168.10.128/26 | 192.168.10.129 ~ 190 | 192.168.10.191 |
| C | 192.168.10.192/27 | 192.168.10.193 ~ 222 | 192.168.10.223 |

---

# VLSM 계산 순서

1. 필요한 Host 수 확인

2. 가장 큰 Host부터 정렬

3. Host Bit 계산

공식

```text
2^(Host Bit) - 2 >= 필요한 Host 수
```

4. CIDR 결정

5. 순서대로 Subnet 할당

---

# VLSM과 FLSM 비교

| 구분 | FLSM | VLSM |
| ------ | ------ | ------ |
| Subnet 크기 | 동일 | 서로 다름 |
| IP 효율 | 낮음 | 높음 |
| 관리 난이도 | 쉬움 | 복잡 |
| 사용 목적 | 단순 분할 | 효율적인 주소 관리 |