## 3-Way Handshake와 4-Way Handshake

3-Way Handshake 는 TCP의 접속, 4-Way Handshake는 TCP의 접속 해제 과정

### TCP의 3-Way Handshake 개념

- TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정(Connection Establish) 하는 과정
- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
즉, TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

### 3-way handshake의 기본 매커니즘

TCP 통신은 PAR (Positive Acknowledgement with Re-transmission) 을 통해 신뢰적인 통신을 제공한다.

PAR을 사용하는 기기는 ack을 받을 때까지 데이터 유닛을 재전송한다!

수신자가 데이터 유닛(세그먼트)이 손상된것을 확인하면(Error Detection에 사용되는 transport layer의 checksum을 활용), 해당 세그먼트를 없앤다. 그러면 sender는 positive ack이 오지 않은 데이터 유닛을 다시 보내야한다.

⇒ 이 과정에서 클라이언트와 서버 사이에서 3개의 Segment가 교환되는 것을 확인할 수 있다. 이것이 바로 3-way handshake의 기본 매커니즘이다.

### 3-way hanshake 동작방식

**Step1 [Client -> SYN -> Server]**  
Client가 Server에게 접속을 요청하는 SYN플래그를 보낸다.  
 
**Step2. [Server -> SYN + ACK -> Client ]**  
Server는 Listen상태에서 SYN이 들어온 것을 확인하고 SYN_RECV상태로 바뀌어 SYN + ACK플래그를 Client에게 전송한다. 그 후 Server는 다시 ACK 플래그를 받기 위해 대기상태로 변경된다.  
 
**Step3. [Client -> ACK -> Server]**  
SYN + ACK 상태를 확인한 Client는 서버에게 ACK를 보내고 연결 성립(Established)이 된다.   
 
위와 같이 신뢰성을 위해 3번의 핸드쉐이킹을 거쳐 연결을 맺는것을 **3-Way Handshake**라고 한다.

### TCP의 4-Way Handshake개념

4-Way Handshake은 연결을 해제 (Connecntion Termination)하는 과정이다. 여기서는 FIN 플래그를 이용한다.
FIN (finish) : 세션을 종료시키는데 사용되며, 더 이상 보낸 데이터가 없음을 나타낸다.

### 4-way Handshake 동작방식


**Step1 [Client -> FIN -> Server]**  
Client가 연결을 종료하겠다는 FIN플래그를 전송한다. 보낸 후에 FIN-WAIT-1 상태로 변한다.  
 
**Step2 [Server-> ACK -> Client]**  
FIN 플래그를 받은 Server는 확인메세지인 ACK를 Client에게 보내준다. 그 후 CLOSE-WAIT상태로 변한다. Client도 마찬가지로 Server에서 종료될 준비가 됐다는 FIN을 받기위해  FIN-WAIT-2 상태가 된다.  
 
**Step3 [Server -> FIN -> Client]**  
Close준비가 다 된 후 Server는 Client에게 FIN 플래그를 전송한다.  
 
**Step4 [Client -> ACK-> Server]**  
Client는 해지 준비가 되었다는 정상응답인 ACK를 Server에게 보내준다. 이 때, Client는 TIME-WAIT 상태로 변경된다.  
   
여기서 TIME-WAIT 상태는 의도치않은 에러로 인해 연결이 데드락으로 빠지는 것을 방지하기 위해 변경 되는 것인데, 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 CLOSED 상태로 변경된다.
