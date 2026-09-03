# Switch

## 개요

Switch는 동일 네트워크 내의 장치들을 연결하고 데이터를 전달하는 Layer 2 장비이다.

MAC Address를 기반으로 목적지를 식별하여 프레임(Frame)을 전달한다.

---

## Switch란?

* OSI 7계층의 Data Link Layer(Layer 2)에서 동작
* MAC Address를 이용하여 통신
* 여러 장치를 하나의 LAN으로 연결
* Collision Domain을 포트별로 분리
* MAC Address Table을 생성하여 목적지 포트로만 데이터 전송

---

## MAC Address Table

스위치는 수신한 프레임의 출발지 MAC 주소를 학습하여 MAC Address Table을 생성한다.

예시

```text
MAC Address          Port
--------------------------
AAAA.AAAA.AAAA       Fa0/1
BBBB.BBBB.BBBB       Fa0/2
CCCC.CCCC.CCCC       Fa0/3
```

---

## Switch 동작 과정

### 1. Learning

출발지 MAC 주소를 학습하여 MAC Table에 저장한다.

### 2. Forwarding

목적지 MAC 주소가 MAC Table에 존재하면 해당 포트로만 전송한다.

### 3. Flooding

목적지 MAC 주소를 모르면 수신 포트를 제외한 모든 포트로 전송한다.

### 4. Filtering

목적지 MAC 주소가 동일 포트에 존재하면 프레임을 폐기한다.

---

## Hub와 Switch 비교

| 구분               | Hub      | Switch      |
| ---------------- | -------- | ----------- |
| 계층               | Layer 1  | Layer 2     |
| 주소 사용            | 없음       | MAC Address |
| 전송 방식            | 모든 포트 전송 | 목적지 포트 전송   |
| Collision Domain | 공유       | 포트별 분리      |
| 성능               | 낮음       | 높음          |

---

## 핵심 정리

* Switch는 Layer 2 장비이다.
* MAC Address를 기반으로 프레임을 전달한다.
* MAC Address Table을 학습하여 통신한다.
* 목적지 MAC을 모르면 Flooding을 수행한다.
* Hub보다 효율적으로 데이터를 전달한다.
