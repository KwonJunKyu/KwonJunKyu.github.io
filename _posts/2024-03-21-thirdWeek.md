---
layout: single
title: "3주차: HTTP와 SMTP"
categories: lecture
tags: [Abstraction, socket, URL, XML, HTTP, TCP/IP]
typora-root-url: ../
---

PPT chapter 2-1. 20p. ~ chpater 2-2. 49p.

### 1. Socket

- #### 개념

  우리가 평소 220V 전력을 사용할 때 발전기에서 직접 끌어다 쓰지 않는다. 그저 콘센트에 꽂기만 하면 어떻게 발전, 변압, 송신하는지 알 필요 없이 전력을 사용할 수 있다. 소켓 또한 같은 개념이다. 우리가 어플리케이션을 개발하고 인터넷을 직접 제어하지 않고 그저 OS에 소켓을 열어달라고만 하면 통신을 시작할 수 있다. API나 함수 같이 간편하게 이용할 수 있다.

- #### Socket 구조

  ![socket architecture](/images/2024-03-21-thirdWeek/socket architecture.png)

  각 함수의 설명은 다음과 같다.

  | 함수 호출 |                             설명                             |
  | :-------: | :----------------------------------------------------------: |
  | Socket()  |                          소켓 생성                           |
  |  Bind()   |              소켓을 위한 특정 인터넷 주소 할당               |
  | Listen()  |                          연결 대기                           |
  | Connect() |            서버에 연결 시도 **(클라이언트 전용)**            |
  | Accept()  | 클라이언트로부터 데이터를 받을 준비가 됐음을 알림 **(서버 전용)** |
  |  Write()  |                         데이터 전송                          |
  |  Read()   |                         데이터 수신                          |
  |  Close()  |                          연결 종료                           |

### 2. IP와 Port

<img src="/images/2024-03-21-thirdWeek/IP-ADDRESS-AND-PORT-NUMBER.webp" alt="IP-ADDRESS-AND-PORT-NUMBER" style="zoom:50%;" />

- #### IP

  동적, 정적, 사설 IP와 같이 쓰임새에 따라 IP를 설정하기도 한다. 동적 IP는 학생이 학교 WiFi에 IP 주소를 요청했을 때 DHCP(Dynamic Host Configuration Protocol)가 IP를 하나 할당해주는 것을 예시로 들 수 있다. 사설 IP는 하나의 기관 내에서 사용하기 위한 것으로, 집에 할당된 IP 주소는 하나이지만 우리가 이용하는 호스트 IP는 다양한 것을 예로 들 수 있다.

- #### Port

  포트는 IP 주소로 호스트에 데이터가 도착했을 때 어떤 어플리케이션에 도달해야 하는지를 알려주는 것으로 80은 HTTP, 25는 SMTP로 낮은 번호 수는 이미 정해진 어플리케이션이 있어 할당할 수 없다. 하지만 IPv4의 경우 16bit unsigned int까지 허용하므로 **65535**까지 포트 번호를 사용할 수 있으므로 범위 내에 원하는 포트 번호를 이용하면 된다.

### 3. 전송 계층(Transfer layer)의 역할

- #### 전송 계층의 특징

  전송 계층은 다음 네 가지의 중요한 기능을 갖춰야 한다. 

  1. **신뢰성** : 중간에 데이터가 유실되거나 손상을 입게 되면 데이터를 제대로 이용할 수 없으므로 잡음 처리와 통신 오류 후 처리가 중요하다. 
  2. **시간** : 통화나 메세지같은 경우 지연 시간이 적을 수록 효율적이다.
  3. **전송률** : 인터넷 방송이나 화상 채팅의 경우 보내야 하는 데이터는 많은데 실시간으로 소통해야 하므로 최소한의 전송률을 보장해줘야 한다.
  4. **보안** : 금융, 개인 정보와 같이 민감한 내용들이 담긴 데이터들은 암호화가 필수다.

- #### TCP

  TCP는 **신뢰성**이 주된 무기인 만큼 다음과 같은 역할을 수행한다.

  - 흐름 제어 (Flow control) : 서버의 처리량보다 많은 요청이 들어올 경우 큐가 쌓이기 시작하는데 큐의 여유 공간을 서버가 클라이언트에게 데이터를 보낼 때 함께 알려줌으로써 요청을 느리게 하는 등 흐름을 제어한다.
  - 혼잡 제어 (Congetion control) : 패킷이 나가는 양보다 들어오는 양이 많을 경우 데이터가 손실되고 이를 또 처리하기 위해 다시 데이터를 요청하게 되어 다시 데이터가 쌓이는 등 혼잡한 상황을 막기 위해 송신측에서 ACK(수신 확인)를 시간 내에 받지 못하면(Time-out) 보내는 패킷의 양을 줄여 혼잡을 줄임
  - 보안, 실시간, 최소 전송률은 보장하지 않는다. (Application에서 보안을 구현)
  - 통신 준비가 되었는지 패킷 3개를 주고 받는 Hand-Shaking 이라는 준비 과정을 통해 연결 상태를 확인한다.

- #### UDP

  - 데이터를 신뢰성있게 보내지 않는다. 한 번 보내고 확인 절차가 없음
  - 하지만 internet traffic을 줄여준다는 것에 의의가 크다.
  - 한 프레임 정도는 소실되도 괜찮은 영상에 주로 쓰인다. (요즘에는 영상도 TCP를 사용한다.)

  

  \< 확인 안하는 UDP와 Hand-Shaking하는 TCP \>

  ![TCP and UDP](/images/2024-03-21-thirdWeek/TCP and UDP.png)

### 4. HTTP

- #### HTTP 구조

  ![http architecture](/images/2024-03-21-thirdWeek/http architecture.png)

  ![HTTP request message](/images/2024-03-21-thirdWeek/HTTP request message.png)

  HTTP는 버전에 따라 이용방식이 달라지므로 데이터를 요청하거나 상태를 나타내는 **Startline**에 HTTP 버전을 넣는다. 특히 송신측의 Method를 집중해야 하는데 밑에서 더 자세히 다루겠다. 메세지의 정보를 담은 헤더 다음에 구분을 위한 공백, 그리고 본문이 있다.

- #### URL (Uniform Resource Locator)

  ![components of URL](/images/2024-03-21-thirdWeek/components of URL.gif)

  URL은 서버가 가진 파일을 요청하는 구문과 같다. 서버의 도메인, 파일 경로, 요청할 파일, 요청하는 방법을 적어 파일을 요청한다.

- #### HTTP의 지속성

  - #### persistent HTTP

    HTTP 1.1부터 지원한 기술로 서버가 응답을 보내고도 TCP 연결을 유지하여 클라이언트가 object를 즉시 요청할 수 있다.

  - #### non-persistent HTTP

    지속성이 없다는 것은 데이터가 필요할 때 마다 통신을 열었다가 닫는 것을 의미한다. 한 HTML 문서에 다양한 링크(object)가 있을 때 매 object를 클릭할 때 마다 소켓을 열고, 데이터를 주고 받고 소켓을 닫는 일련의 과정을 수행한다. 과거 데이터를 많이 주고받을 수 없었을 때 이용했다.

    

    ![non persistent http](/images/2024-03-21-thirdWeek/non persistent http-1711096391351-12.png)

    

RTT(Round-Trip Time)는 소켓 하나가 왔다갔다 하는 시간을 의미한다. 우선 연결 상태를 확인하는데에 1RTT, 이후 요청하고 받는데 1RTT, 여기에 파일을 보내는 시간까지 합하면 한 번 object를 받는데 걸리는 시간은
$$
응답시간 = 2RTT + 파일 전송 시간
$$
이다.

- #### Message

  - ##### Method types

    | Method |                             의미                             |
    | :----: | :----------------------------------------------------------: |
    |  GET   | 도메인 주소(요청)에 쿼리문등을 추가하여 특정 파일을 **요청** |
    |  POST  |       요청 메세지의 body에 사용자 입력 정보를 **전송**       |
    |  HEAD  |                  문서의 HEADER 부분만 요청                   |
    |  PUT   | 서버의 Resource를 업데이트하기 위해 Client에서 데이터를 **전송** |
    | DELETE |                  서버의 Resource를 **삭제**                  |

  - ##### status codes

    | code |                          의미                          |
    | :--: | :----------------------------------------------------: |
    | 200  |                     요청 처리 성공                     |
    | 301  | 문서가 이동됐고 서버가 이동된 곳을 알 때 전송되는 코드 |
    | 400  |               서버가 이해할 수 없는 요청               |
    | 404  |       요청한 페이지를 찾을 수 없음 (문서가 없음)       |
    | 505  |                지원하지 않는 HTTP 버전                 |

- #### Cookie

  쿠키는 비상태 프로토콜을 상태인 것처럼 만들어주는 것으로, 클라리언트 측이 쿠키를 허용하면 서버에서 특정 번호를 할당해주고 클라이언트가 서버에 요청할 때마다 쿠키 번호를 보내주면 이 번호에 맞춰 정보를 저장한다. 이것을 통해 클라이언트의 정보를 구별함으로써 개인 맞춤화 전략을 수행할 수 있고 정보를 수집할 수 있다.

- #### Caching with Proxy server

  <img src="/images/2024-03-21-thirdWeek/Proxy server.png" alt="Proxy server" style="zoom:50%;" />

  캐쉬처럼 Proxy 서버를 클라이언트와 서버 사이에 두어 통신속도를 보완하고자 한 것으로 위와 같이 글로벌망과는 통신 속도가 느리지만 내부망은 속도가 빠를 경우 중간에 Proxy 서버를 두어 Origin 서버로부터 데이터를 미리 받아놓은 뒤 데이터를 요청받는다. 이때 문서의 내용이 Update 되어 있을 수 있으니 Origin 서버에 업데이트된 날짜를 확인한 후 틀리면 Origin 서버에서 다시 문서를 보내 Update 해준다.

### 5. 이메일 프로토콜

- #### SMTP (Simple Mail Transfer Protocol)

  각 사용자는 SMTP로 통신하는 메일 서버를 이용하여 통신한다. A가 B에게 메세지를 보낸다면 A - A의 메일 서버 - B의 메일 서버 - B 이렇게 메일이 전송된다.

  1. ID에 대한 예시로 abc@dankook.ac.kr과 def@naver.com이 있다면 abc는 dankook 메일 서버, def는 naver 메일 서버를 이용한다
  2. A가 보낸 메일은 dankook 메일 서버에 저장된다.
  3. dankook의 메일 서버는 def@naver.com에 접근하여 naver 메일 서버에 메일을 전송한다.
  4. naver 메일 서버는 ID def에 접근하여 def의 메일함에 메일을 넣는다.

  

  ![smtp example](/images/2024-03-21-thirdWeek/smtp example.png)

- #### MIME (Multipurpose Mail Internet Extensions)

  이메일은 7bit ASCII 코드만 지원하므로 유니코드 등 다양한 문자 체계를 구현하기 위한 해독지같은 것이다. MIME은 유니코드, 그림, 영상 등을 ASCII 문자 체계로 인코딩, 디코딩할 수 있다. 따라서 송/수신측 둘 다 MIME을 이용하여 메세지를 주고받게 된다.

- #### POP과 IMAP

  요새는 잘 쓰이지 않는다.

- #### telnet 명령어

  cmd에서 telnet을 이용하여 해당 포트가 접속 가능한지 알아볼 수 있는데, [제어판] - [프로그램 및 기능 ] - [Windows 기능 켜기/끄기] - [텔넷 클라이언트] 를 체크하면 사용할 수 있다.

  ![스크린샷 2024-03-25 111710](/images/2024-03-21-thirdWeek/스크린샷 2024-03-25 111710.png)

  \< cmd에서 실행해본 모습 \>

  ![스크린샷 2024-03-25 111514](/images/2024-03-21-thirdWeek/스크린샷 2024-03-25 111514.png)
