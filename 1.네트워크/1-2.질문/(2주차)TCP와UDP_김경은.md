# 1️⃣ TCP/UDP

tcp와 udp모두 `4계층=전송계층=Transport Layer` 에서 사용되는 프로토콜이다.

## 🍰 TCP (Transmission Control Protocol)

`신뢰성 있는 전송`이 목표

### TCP 사용처

HTTP, FTP, SMTP 등 신뢰성 있는 전송이 중요한 곳

### 가상 회선 패킷 교환 방식

패킷을 목적지로 전송할 때 가상 회선(경로)을 설정한 후, 경로를 따라서 패킷을 전송하는 방법

따라서 모든 패킷은 `같은 경로` 로 전송된다.

경로를 미리 정한 후 패킷을 보내기 때문에 순서가 보장된다. (유실된다면??)

### 3-way handshaking

TCP가 연결을 수립(`establish`)하는 과정

![Untitled (1)](https://github.com/KangHayeonn/together-party-tonight-server/assets/73164845/81e051ec-938d-4f50-9867-f929a4c86cdf)

기본적으로 SYN를 보내면 응답으로 ACK가 오는 구조

<aside>
💡 1. 클라이언트가 `SYN`를 보냄 (`SYN-SENT` 상태)
2. 서버가 응답으로 `ACK`와 `SYN`를 함께 보냄. (`SYN-RECEIVED` 상태)
3. 서버의 `ACK`를 받고 `ESTABLISHED` 상태가 됨.
4. 서버의 `SYN`에 대한 응답으로 `ACK`를 보냄.
5. 클라이언트의 `ACK`를 받고 `ESTABLISHED`상태로 전환.

</aside>

SYN를 보낼때 클라이언트와 서버의 **ISN**을 함께 보내게 되는데

ISN이란, 새로운 TCP연결의 첫번째 패킷에 할당된 임의의 시퀀스 번호를 말한다.

ACK를 보낼때는 SYN의 **ISN+1**한 값을 보내게 된다.

### 4-way handshaking

TCP가 연결을 해제(`close`)하는 방법

![Untitled (2)](https://github.com/KangHayeonn/together-party-tonight-server/assets/73164845/e1897504-5582-4ad8-8579-00edeb48d3f3)

<aside>
💡 1. 클라이언트가 `FIN`를 보냄 (`FIN_WAIT_1` 상태)
2. 서버가 응답으로 `ACK` 를 보냄. (`CLOSE_WAIT` 상태)
3. 서버도 `FIN`을 보내고 `LAST_ACK` 상태가 됨.
4. 서버의 `FIN`에 대한 응답으로 `ACK`를 보냄. (`TIME_WAIT`상태) → 시간이 지나고 `CLOSED`상태로
5. 클라이언트의 `ACK`를 받고 `CLOSED`상태로 전환.

</aside>

### 🕰️ TIME_WAIT

소켓이 바로 소멸되지 않고 일정 시간 유지 되는 상태

`TIME_WAIT`가 왜 필요할까요?

→ TIME_WAIT없이 클라이언트가 마지막 ACK를 보내고 연결을 종료하였는데 ACK가 중간에 소멸된다면

이를 받지 못한 서버는 일정 시간후 다시 FIN을 클라이언트에게 보내게 됩니다.

그런데 이떄 클라이언트의 소켓은 이미 닫혔으므로 FIN을 받을 수 없고 결과적으로 ACK도 보낼 수 없습니다.→ 서버는 계속 대기하게 되고 연결을 정상적으로 종료할 수 없음.

## 🍧 UDP (User Datagram Protocol)

`빠른 전송`이 목표

### UDP 사용처

스트리밍 서비스(유튜브), 전화같이 중간에 조금 끊겨도 되지만 빠른 전송을 해야하는 경우

### 데이터 그램 패킷 교환 방식

패킷을 목적지로 전송할 때 각 패킷이 독립적으로 움직이는 방법

각 패킷은 그때 그때 적절한 경로를 선택하여 목적지까지 도달한다. 따라서 패킷별로 이동 경로가 다를 수 있다.

## 정리
|  | TCP | UDP |
| --- | --- | --- |
| 패킷 전송 방식 | 가상 회선 방식 | 데이터그램 패킷 교환 방식 |
| 연결 여부 | 연결 O | 연결 X |
| 패킷의 순서 | 순서대로 도착함을 보장 | 순서가 보장되지 않음 |
| 신뢰성 | 수신 여부 확인 O | 수신 여부 확인 X |
| 오류 제어 | 체크섬 방식, 응답 패킷, Go back N , Selective repeat | 체크섬 방식  |
| 흐름 제어 | 슬라이딩 윈도우 | 불가 |
| 혼잡 제어 | Slow start, Congestion Avoidance, fast retransmit, fast recovery | 불가 |
| 순서제어 | 가능 | 불가 |


# 🫣 면접 예상 질문
1. TCP/ UDP 프로토콜에 대해 설명해보세요
2. 3 way handshaking과 4 way handshaking에 대해 설명해보세요
3. 4 way handshaking에서 time_wait이 왜필요한지 설명해보세요