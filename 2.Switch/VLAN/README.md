# VLAN (Virtual LAN)

## 개요
VLAN(Virtual LAN)은 하나의 물리적인 스위치를 여러 개의 논리적인 네트워크로 분리하는 기술이다.

같은 스위치에 연결되어 있더라도 서로 다른 VLAN에 속한 장치들은 직접 통신할 수 없다.

---

## VLAN이란?

- Virtual Local Area Network의 약자
- Layer 2에서 논리적인 네트워크 분리
- Broadcast Domain 분리
- 네트워크 보안성 향상
- 관리 효율성 증가
- 하나의 스위치를 여러 개의 독립된 스위치처럼 사용 가능

---

## VLAN이 필요한 이유

### 1. Broadcast Domain 분리

스위치는 기본적으로 하나의 Broadcast Domain을 가진다.

VLAN을 구성하면 VLAN마다 독립적인 Broadcast Domain이 생성된다.

예시

```text
VLAN 10
 ├─ PC1
 └─ PC2

VLAN 20
 ├─ PC3
 └─ PC4
```

PC1이 브로드캐스트를 전송하면 VLAN 10에 속한 PC2만 수신한다.

PC3, PC4는 브로드캐스트를 받지 않는다.

---

### 2. 보안 향상

서로 다른 부서를 VLAN으로 분리하면 불필요한 접근을 제한할 수 있다.

예시

```text
VLAN 10 : 인사부
VLAN 20 : 개발부
VLAN 30 : 회계부
```

각 VLAN은 독립적으로 동작한다.

---

### 3. 관리 효율 향상

사용자가 다른 위치로 이동하더라도 동일한 VLAN에 할당하면 기존 네트워크 정책을 그대로 사용할 수 있다.

---

## VLAN ID

VLAN은 VLAN ID를 이용하여 구분한다.

| VLAN ID | 설명 |
|----------|----------|
| 1 | 기본 VLAN (Default VLAN) |
| 2 ~ 1001 | 일반 VLAN |
| 1002 ~ 1005 | 예약 VLAN |
| 1006 ~ 4094 | Extended VLAN |

예시

```text
VLAN 10 : 영업부
VLAN 20 : 개발부
VLAN 30 : 서버실
```

---

## Access Port

Access Port는 하나의 VLAN에만 소속될 수 있는 포트이다.

일반적으로 PC, 서버, 프린터 등이 연결된다.

예시

```text
PC ─── Fa0/1
         │
      VLAN 10
```

설정 예시

```bash
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

---

## VLAN 통신

### 같은 VLAN

```text
PC1 (VLAN 10)
      │
   Switch
      │
PC2 (VLAN 10)
```

통신 가능

### 다른 VLAN

```text
PC1 (VLAN 10)
      │
   Switch
      │
PC2 (VLAN 20)
```

통신 불가능

VLAN이 다르면 서로 다른 Broadcast Domain에 속하기 때문이다.

---

## Inter-VLAN Routing

서로 다른 VLAN 간 통신을 위해서는 Layer 3 장비가 필요하다.

예시

```text
VLAN 10 ── Router ── VLAN 20
```

또는

```text
VLAN 10 ── Layer 3 Switch ── VLAN 20
```

이를 Inter-VLAN Routing이라고 한다.

---

## VLAN 생성 및 확인

### VLAN 생성

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
```

### VLAN 목록 확인

```bash
Switch# show vlan brief
```

---

## Switch와 VLAN 비교

| 구분 | 일반 Switch | VLAN 적용 Switch |
|--------|--------|--------|
| Broadcast Domain | 1개 | VLAN별 분리 |
| 보안성 | 보통 | 높음 |
| 트래픽 효율 | 보통 | 높음 |
| 네트워크 관리 | 단순 | 유연 |
