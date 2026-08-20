# MTU

## 개요

**L2계층에서 한번에 전송할 수 있는 최대 패킷의 크기**를 뜻한다.<br>
IP헤더와 상위데이터의 합산이며 L2이더넷 헤더는 포함되지 않는다.<br>
최대크기는 **1500Byte**이다.

---

# IP Fragmentation

## 예시

<p align="center">
  <img src="./Image/ip_fragmentation.png">
</p>

## IP Fragmentation 과정
IP패킷의 크기가 MTU보다 클 경우 패킷을 여러개의 작은 조각으로 쪼갠다.<BR>
예를들어 L3패킷의 크기가 4000Byte일 경우 해당 패킷을 L2계층의 MTU에 맞게 쪼개서 보내게 된다.<BR>
이때 1500Byte의 제한 안에는 데이터를 목적지까지 안내할 IP헤더가 포함되어야 하므로




