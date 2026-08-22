# 01. OSI 7 Layer & TCP/IP

## 개요

OSI 7 Layer는 네트워크 통신 과정을 7개의 계층으로 나누어 표준화한 참조 모델이다.

각 계층은 독립적인 역할을 수행하며, 상위 계층은 하위 계층의 서비스를 이용하여 데이터를 전송한다.

---

## OSI 7 Layer

| Layer | Name         | Device     | PDU     |
| ----- | ------------ | ---------- | ------- |
| 7     | Application  | -          | Data    |
| 6     | Presentation | -          | Data    |
| 5     | Session      | -          | Data    |
| 4     | Transport    | -          | Segment |
| 3     | Network      | Router     | Packet  |
| 2     | Data Link    | Switch     | Frame   |
| 1     | Physical     | Hub, Cable | Bit     |

---

## Layer 7 - Application

사용자와 가장 가까운 계층으로 네트워크 서비스를 제공한다.

### 대표 프로토콜

* HTTP
* HTTPS
* FTP
* DNS
* SMTP

---

## Layer 6 - Presentation

데이터 형식 변환 및 암호화를 담당한다.

### 주요 기능

* 인코딩
* 암호화
* 압축

---

## Layer 5 - Session

통신 세션을 생성하고 유지한다.

### 주요 기능

* 세션 생성
* 세션 유지
* 세션 종료

---

## Layer 4 - Transport

종단 간 통신을 담당한다.

### 대표 프로토콜

* TCP
* UDP

### 주요 기능

* 흐름 제어 (Flow Control)
* 오류 제어 (Error Control)
* 신뢰성 보장

---

## Layer 3 - Network

논리적 주소(IP)를 이용하여 목적지까지 경로를 결정한다.

### 대표 장비

* Router

### 대표 프로토콜

* IP
* ICMP
* OSPF
* RIP

---

## Layer 2 - Data Link

MAC Address를 이용하여 동일 네트워크 내에서 통신한다.

### 대표 장비

* Switch
* Bridge

### 주요 기능

* Frame 전송
* MAC Address 학습
* 오류 검출

---

## Layer 1 - Physical

실제 전기적 신호를 전송하는 계층이다.

### 대표 장비

* Hub
* Repeater
* Cable

---

## Encapsulation

데이터가 송신될 때 각 계층의 헤더가 추가되는 과정이다.

```text
Application Data
      ↓
Transport Header + Data
      ↓
Network Header + Segment
      ↓
Data Link Header + Packet
      ↓
Frame
```

---

## TCP/IP Model

| TCP/IP Model   | OSI Model   |
| -------------- | ----------- |
| Application    | Layer 7 ~ 5 |
| Transport      | Layer 4     |
| Internet       | Layer 3     |
| Network Access | Layer 2 ~ 1 |

---

## OSI vs TCP/IP

| OSI Model       | TCP/IP Model    |
| --------------- | --------------- |
| 7 Layers        | 4 Layers        |
| Reference Model | Practical Model |
| Theory-based    | Internet-based  |

---

## 데이터 단위 정리

* Layer 1 → Physical → Bit
* Layer 2 → Data Link → Frame
* Layer 3 → Network → Packet
* Layer 4 → Transport → Segment
* Layer 7 → Application → Data
