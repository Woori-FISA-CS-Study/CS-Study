
 ## DNS (Domain Name System) 란?
- 도메인 네임 시스템 (Domain Name System, DNS) 은 호스트의 도메인네임 (www.example.com)을 네트워크주소(192.168.1.0)로 변환하거나, 그 반대의 역할을 수행하는 시스템이다.
예를 들면 우리가 자주 접하는 naver.com , google.com 모두 DNS을 가진 DN(Domain Name)이라고 할 수 있다.
이들은 사실 문자열의 탈을 쓴 IP이다.

![캡처](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/b40e8ce2-8b52-427b-96f7-ebd2d89ee00f)





### 참고 (www.naver.com 을 입력했을때 DNS 동작과정)
1. 웹 브라우저에 www.naver.com을 입력 -> PC에 저장된 **Local DNS**(기지국 DNS 서버)에게 "www.naver.com"이라는 hostname에 대한 IP 주소를 요청  
2. Local DNS는 **Root DNS** 서버에게 "www.naver.com 의 IP 주소"를 요청
4.  Root DNS 서버 는 "www.naver.com 의 IP 주소" 를 찾을 수 없어 Local DNS 서버에게 "www.naver.com 의 IP 주소 찾을 수 없다고 다른 DNS 서버에게 물어봐" 라고 응답.
5.  Local DNS 서버는com 도메인을 관리하는 **TLD DNS 서버 (최상위 도메인 서버)** 에 다시 www.naver.com에 대한 IP 주소를 요청
6. com 도메인을 관리하는 DNS 서버에도 해당 정보가 없으면, Local DNS 서버에게 "www.naver.com 의 IP 주소 찾을 수 없음. 다른 DNS 서버에게 물어봐" 라고 응답.
6. 이제 Local DNS 서버는 naver.com **DNS 서버(AuthoritativeDNS 서버)** 에게 다시 "www.naver.com 의 IP 주소" 를 요청. 
7. naver.com DNS 서버 에는 "www.naver.com 의 IP 주소" 가 있다.  
그래서 Local DNS 서버에게 "www.naver.com에 대한 IP 주소는 222.122.195.6" 라는 응답을 한다.  
 
8. 이를 수신한 Local DNS는 www.naver.com 의 **IP 주소를 캐싱**을 하고 이후 다른 요청이 있을시 응답할 수 있도록 IP 주소 정보를 단말(PC)에 전달해 준다.


### Local DNS(기지국 DNS 서버) 란?  
기본적으로 인터넷을 사용하기 위해선 IP를 할당해주는 통신사(KT, SK, LG 등...)에 등록하게 된다.컴퓨터의 LAN선을 통해 인터넷이 연결되면, 가입했던 각 통신사의 기지국 DNS 서버가 등록되게 된다.

### Root DNS(루트 네임서버) 란?  
Root DNS는 인터넷의 도메인 네임 시스템의 루트 존이다. ICANN이 직접 관리하는 절대 존엄 서버로, 
TLD DNS 서버 IP들을 저장해두고 안내하는 역할을 한다.전세계에 961개의 루트 DNS가 운영되고 있다.

### TLD(Top-Level Domain, 최상위 도메인) DNS Server 란?  
TLD는 도메인 등록 기관(Registry)이 관리하는 서버로, 도메인 네미의 가장 마지막 부분을 말한다.예를들어 웹사이트에서 한번쯤은 봐왔던 .com 이나 co.kr 같은 도메인들을 관리하고 부여하는 서버이다.
Authoritative DNS 서버 주소를 저장해두고 안내하는 역할을 한다.

### InfoAuthoritativeDNS Server 란?  
실제 개인 도메인과 IP 주소의 관계가 기록/저장/변경되는 서버.그래서 권한의 의미인 Authoritative가 붙는다.
일반적으로 도메인/호스팅 업체의 ‘네임서버’를 말하지만, 개인이나 회사 DNS 서버 구축을 한 경우에도 여기에 해당하게 된다.


### 재귀적 쿼리 Recursive Query
 Local DNS 서버가 여러 DNS 서버에 차례대로 (Root DNS 서버 → TLD DNS 서버(.com) → Authoritative DNS 서버(naver.com) 요청하여 
그 답을 찾는 과정.

### 질문
dns 동작과정 순서
1. tld서버 2. root서버 3. local dns서버 4.authoritaive 서버  
