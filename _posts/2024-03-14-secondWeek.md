---
layout: single
title: "2주차: 네트워크 코어/구조/보안, HTTP"
categories: lecture
tags: [Abstraction, Protocol, TCP/IP, P2P]
typora-root-url: ../
---

PPT chapter 1. 34p. ~ chpater 2-1. 20p.

### 1. 네트워크 코어

- #### 네트워크 코어의 정의

  네트워크 코어는 인터넷을 구축하는 스위치와 링크의 집합으로 우리가 인터넷을 사용할 때 어떻게 데이터가 전송되는지를 결정하는 시스템이다. 회선 교환 방식과 패킷 교환 방식, 두 가지로 나뉘는데 각각의 장단점과 적용 분야가 있으므로 상황에 맞춰 사용한다.
  
- #### 회선 교환 (Circuit Switching)

  과거 전화국에서 쓰였던 회선 교환 방식은 두 사용자 사이에 수많은 경로 중 **하나의 전용 경로**를 전담해주어 정보를 교환하는 방식이다.

  |                             장점                             |                             단점                             |
  | :----------------------------------------------------------: | :----------------------------------------------------------: |
  | 1. 데이터 송/수신의 신뢰도가 높다.<br />2. 데이터가 공유되지 않는다. | 1. 통신이 이루어지지 않을 경우 자원이 낭비된다.<br />2. 비싸다. |

  

  하나의 물리적 케이블 사용하기 때문에 다수가 이용하려면 다음과 같은 분할화 작업이 필요하다.

  |            FDM (Frequency Division Multiplexing)             |       TDM (Time Division Multiplexing)       |
  | :----------------------------------------------------------: | :------------------------------------------: |
  |         선로의 주파수 대역을 나누어 사용하게끔한다.          | 특정 시간에 정해진 사용자가 사용하도록 한다. |
  |                       간섭에 취약하다                        |                간섭에 강하다.                |
  |                  아날로그 통신만 가능하다.                   |     아날로그/디지털 통신 둘 다 가능하다.     |
  | 간섭을 막기 위해서 일종의 완충지역 역할을 하는 Guard Band가 필요하다. |     두 사용자 간 동기화 펄스가 필요하다.     |

  <img src="/images/2024-03-14-secondWeek/FDM TDM.png" alt="FDM TDM" style="zoom: 33%;" />

  

- #### 패킷 교환 (Packet Switching)

  패킷 교환 방식은 데이터를 작은 패킷으로 나눈 후 다양한 경로를 거쳐 최종 목적지에 도달시키는 것을 의미한다. 패킷이 거칠 경로를 탐색하는 **라우팅** 기술과 라우터가 받은 패킷을 올바른 곳에 출력하는 **포워딩(전달)** 기술이 필요하다.

  |                             장점                             |                             단점                             |
  | :----------------------------------------------------------: | :----------------------------------------------------------: |
  | 1. 자원을 효율적으로 사용할 수 있다.<br />2. 확장성과 유연성이 뛰어나다.<br />3. 저렴하다. | 1. 네트워크 지연에 따른 손실이 발생할 수 있다.<br />2. 여러 경로를 거치고 지연 가능성이 있어 대기 시간이 더 길다. |

- #### 패킷 교환 VS 회선 교환

  패킷 교환은 선로의 효율적 사용으로 회선 교환보다 **많은 사용자를 수용**할 수 있지만 **복잡한 프로토콜**이 필요하며 패킷 전송의 대기 시간 및 데이터의 손실 가능성 때문에 **실시간 통신(음성, 비디오)에는 적합하지 않다.**

  [더 자세한 정보](https://www.geeksforgeeks.org/difference-between-circuit-switching-and-packet-switching/)



### 2. 인터넷의 구조

- #### Access network

  Access network(접속망)는 **종단 시스템의 첫 번째 라우터까지의 LAN**을 의미한다. 이 LAN들끼리 통신하기 위해서 각 Access network를 각각 모두 연결해주는 것은 O(N^2)만큼의 자원이 소모되는 것으로, 하나의 Access network를 추가하거나 삭제하기만 해도 비용이 높게 든다.

- #### ISP

  따라서 이걸 대신해주는 것이 **ISP(Internet Service Provider), 인터넷에 접속할 수 있도록 서비스를 제공하는 기업이나 기관**이다.

  하지만 단 하나의 ISP만 존재하여 독점 시스템을 구축한다면 사용자에게 압박을 줄 수 있으므로 3개 이상의 ISP들이 네트워크 망을 구축한다. 그럼 이들 사이에도 통신하는 Peering Link가 있어야 하는데, 이를 **IXP(Internet Exchange Point)**가 수행한다.

  ISP에 접속하기 전에 **지역 네트워크 망(Regional network)**에 모이기도 한다.

  또한 Google이나 Netflix 같이 자신의 서비스를 제공하기 위해 많은 트래픽을 소모하는 기업의 경우 일반 ISP를 이용하면 일반 사용자들에게 피해를 줄 수 있기 때문에 자체적으로 고속전용회선(Content Provider network)을 구축한다.

  ![network by tier](/images/2024-03-14-secondWeek/network by tier.png)

  

  <img src="/images/2024-03-14-secondWeek/internet structurepng.png" alt="internet structurepng" style="zoom:33%;" />

### 3. 패킷 지연과 손실

### 4. 프로토콜의 계층

### 5. 네트워크 보안

- #### malware

- #### DOS 공격

### 6. 인터넷의 역사 (대표적으로)

- 1961년 : Kleinrock – 큐잉 이론으로 패킷 교환의 효율성을 보임

- 1969년 : 최초의 ARPAnet 노드가 동작

- 1974년 : Cerf 와 Kahn의 internetworking 원칙

  - minimalism, autonomy – 네트워크 상호연결을 위해 내부변경을 요구하면 안됨

  - best effort 서비스 모델

  - stateless routers

  - decentralized control

- 1983년 : TCP/IP 프로토콜 채택

- 1983년 : DNS 정의

- 1990년대 초반 : Berners-Lee HTML, HTTP, Mosaic

### 7. TCP/IP 계층도

![TCP IP layer](/images/2024-03-14-secondWeek/TCP IP layer.png)

- 

### 8. TCP/IP Application 계층

- 사용되는 언어
- Server/Client
- P2P

### 9. Cloud Computing
