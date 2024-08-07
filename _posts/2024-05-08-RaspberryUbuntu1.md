---
layout: single
title: "라즈베리파이로 우분투 웹 서버 구현하기 (1) : 라즈베리파이 초기 설정"
categories: RaspberryPi
tags: [RaspberryPi, Ubuntu, WebServer]
typora-root-url: ../
---





## 서론

#### 대학교 2학년, 뭔가 할 수 있는 프로젝트가 없을까?

대학교 1학년을 마치고 2학년에 들어선 지금, 언어에 대한 기초는 탄탄하게 잡혀있지 않나 싶습니다. 최소한 어떤 코드를 봤을 때 한 순간에 이해되지는 않아도 차근차근 접근하면 이해할 수 있는 지식 기반을 갖춘 것이죠. 하지만 이 지식은 코드를 알아볼 수 있음에 그치는 것이지 직접 새로운 창작물을 만들 수 있다는 '진정한 이해'에 도달하지는 못했다고 생각합니다. 우리가 배운 언어가 어떻게 쓰이는지는 알지만 어떻게 쓰는지는 모르기에 내가 만들고 싶은 것이 있어도 어디서부터 시작해야 할지 감도 잡히지 않습니다. 그래서 시도조차 해보지 않으면 아무것도 없다는 세상의 이치에 따라 제가 하고 싶었던 프론트엔드를 하기 위해 직접 백엔드를 만들어보기로 했습니다(!!).

#### AWS보다 가까운 나의 서버, 라즈베리파이

이 생각이 들자마자 문득 라즈베리파이가 떠올랐습니다. '구석에 짱 박혀서 구동하지도 않는 이 친구를 활용하고 싶다..!'라는 의지가 타오른거죠. AWS라는 아주 좋은 서비스가 있지만 시간이 지나면 유료가 된다는 점과 진정 깊은 코드를 이해하기 위해선 직접 만드는 게 좋지 않을까? 라는 무모한 생각과 추측으로 시작해보는 **라즈베리파이 웹 서버**입니다.

<img src="/images/2024-05-08-RaspberryUbuntu1/짱박혀있던라즈베리파이.jpg" alt="짱박혀있던라즈베리파이" style="zoom: 25%;" />



------



## 라즈베리파이에 Ubuntu Server 설치



우선 라즈베리파이에 Ubuntu를 설치해야겠죠! 



<img src="/images/2024-05-08-RaspberryUbuntu1/스크린샷 2024-07-05 033831.png" alt="스크린샷 2024-07-05 033831" style="zoom:33%;" />

<img src="/images/2024-05-08-RaspberryUbuntu1/스크린샷 2024-07-05 033900.png" alt="스크린샷 2024-07-05 033900" style="zoom:33%;" />

<img src="/images/2024-05-08-RaspberryUbuntu1/스크린샷 2024-07-05 033903.png" alt="스크린샷 2024-07-05 033903" style="zoom:33%;" />

<img src="/images/2024-05-08-RaspberryUbuntu1/스크린샷 2024-07-05 033911.png" alt="스크린샷 2024-07-05 033911" style="zoom:33%;" />
