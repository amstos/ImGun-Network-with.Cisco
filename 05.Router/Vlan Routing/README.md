# Vlan Routing

## 개요
**Vlan Routing**은 하나의 물리적인 스위치를 여러 개의 논리적인 네트워크로 분리한 Vlan을 서로 통신이 가능하도록 만드는 기술이다.

VLAN은 기본적으로 L2 이므로 다른 VLAN과는 통신할 수 없다 때문에 서로 통신이 가능하도록 L3의 기술이 필요하다

---
## VLAN 간 라우팅 방식

### Router-on-a-Stick

- 하나의 물리 포트를 **서브인터페이스로 나눠** 여러 VLAN을 처리
- **L2 스위치 + 라우터** 조합
<p align="center">
  <img src="./Image/router_subinterface.png">
</p>

---
