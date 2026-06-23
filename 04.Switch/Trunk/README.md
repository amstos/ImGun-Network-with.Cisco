# 06. Trunk Port

## 개요

Trunk Port는 여러 VLAN의 트래픽을 하나의 링크로 전달하기 위한 포트이다.

주로 스위치와 스위치 간 연결에 사용된다.

---

## Trunk Port란?

- 여러 VLAN을 동시에 전달
- VLAN 정보를 유지하며 전송
- 주로 네트워크 장비 간 연결에 사용
- IEEE 802.1Q 표준 사용

---

## VLAN Tagging

Trunk Port는 프레임에 VLAN 정보를 추가하여 전송한다.

이를 VLAN Tagging이라고 한다.

수신 장비는 VLAN Tag를 확인하여 해당 VLAN으로 전달한다.

예시

```text
VLAN 10 → Tag 추가
VLAN 20 → Tag 추가
VLAN 30 → Tag 추가
```

---

## Native VLAN

Native VLAN은 VLAN Tag 없이 전송되는 VLAN이다.

기본값은 VLAN 1이다.

예시

```text
VLAN 1  → Tag 없음
VLAN 10 → Tag 추가
VLAN 20 → Tag 추가
```

---

## 설정 예시

```bash
Switch(config)# interface g0/1
Switch(config-if)# switchport mode trunk
```

---

## 확인 명령어

```bash
Switch# show interfaces trunk
```

---

## Access Port와 Trunk Port 비교

| 구분 | Access Port | Trunk Port |
|--------|--------|--------|
| VLAN 수 | 1개 | 여러 개 |
| 연결 대상 | PC | 스위치, 라우터 |
| VLAN Tag | 사용 안 함 | 사용 |