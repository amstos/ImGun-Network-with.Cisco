# Spanning Tree Protocol

## 개요

Spanning Tree Protocol은 스위치에서 루프를 방지하기 위해 사용하는 Layer 2 프로토콜이다.

---

# 주요 목적
- 네트워크 루프 방지
- 네트워크 안정성 향상
- 중복 경로 관리

# 스패닝트리를 이해하기 위해서는 알아야 하는 지식
- 브리지ID(BID): 브리지ID는 스위치(브리지)들이 통신 할 때 서로를 확인하기 위해 하나씩 가지고 있는 번호이다.
- BID는 64bit중 16bit의 브리지 우선순위(Bridge Priority)와 48bit의 MAC Address로 이루어져 있다.
- Path Cost: 한 스위치에서 다른 스위치로 가는 데 드는 비용이다.
- 스위치는 스패닝 트리 프로토콜을 위해'BPDU'라는 프레임을 사용한다 이 BPDU에는 Root BID, Root Path Cost, Sender BID, Port ID가 있다.
# 작동 방식

STP는 다음과 같은 단계로 작동한다.
1. 루트 브리지 선출: 가장 낮은 BID를 가진 스위치를 루트 브리지 선정
2. 루트 포트 선정: 각 NON-루트 브리지에서 루트 브리지까지의 최적 경로 결정
3. 지정 포트 선정: 각 세그먼트에서 루트 브리지로의 최적 경로 제공
4. 블로킹 포트 설정: 루프 방지를 위해 나머지 포트를 차단
# 포트 상태
- Blocking: 데이터 전송 불가, BPDU만 수신
- Listening: 데이터 전송 불가, BPDU 송수신
- Learning: MAC 주소 학습 시작, 데이터 전송은 불가
- Forwarding: 정상적인 데이터 전송 상태
- Disabled: 관리자에 의해 비활성화된 상태
# 예시
<p align="center">
  <img src="image/IMG_0015.PNG" width="550">
</p>
위 상태일때 스위치 A,B,C는 서로간의 BPDU를 주고받고 스위치 A가 루트브리지로 선정된다.

이후 스위치A와B는 루트 포트 선정을 하는데 루트 브리지에 가장 가까이 있는(Path Cost가 가장 낮은) 포트가 루트 포트가 된다.</br>
다음 지정 포트(Designated Port)를 선정하는데 지정포트는 한 세그먼트당 하나의 지정포트를 갖는다 선정 과정은 루트 브리지까지의 Path Cost 즉 세그먼트 상에서 Root Paht Cost를 서로 비교해서 더 작은 Root Path Cost를 가진 포트가 지정 포트가 된다.</BR>
하지만 위 상태에서 스위치B와 스위치C는 서로 같은 Cost를 갖기에 다음 단계인 서로의 BID를 비교하여 더 낮은 BID를 가진 스위치 B의 포트가 지정 포트로 선정된다.

최종적으로는 이런 형태가 된다.
<p align="center">
  <img src="image/IMG_0016.PNG" width="550">
</p>