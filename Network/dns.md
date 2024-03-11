>   ## DNS(Domain Name System)
>   IP 주소는 IPv4 기준 12개 숫자와 .으로 구성되어 있어 외우기가 힘들다. 이를 좀 더 알아보기 쉽게 'naver.com', 'google.com'과 같이 문자와 .으로 표현한 주소를 도메인 이름(Domain Name)이라고 한다.   
>   네트워크에서 이러한 도메인 이름을 숫자로 된 IP 주소로 변환해주는 TCP/IP 서비스를 DNS라 하며 계층 구조를 가지는 분산데이터베이스 구조이다.

## DNS 작동 원리

1. Local DNS 서버에 "www.naver.com"에 대해 query

2. Local DNS 서버에 정보가 없다면 Root DNS 서버에 query

3. Root DNS 서버(Root Name Server)에서 "com 도메인"을 관리하는 TLD Name 서버 정보 전달

4. TLD Name 서버에 query

5. TLD Name 서버에서 "naver.com" 관리하는 DNS 정보 전달

6. "naver.com" 도메인을 관리하는 DNS 서버에 "www.naver.com"에 대한 IP 주소 query

7. Local DNS 서버에게 222.122.195.6 응답

8. Local DNS는 www.naver.com에 대한 IP 주소를 캐싱하고 IP 주소 정보 전달

## DNS Server

### Local DNS Server (Recursive DNS Server)

사용자가 가장 먼저 접근하는 DNS 서버. DNS 쿼리를 통해 얻은 데이터를 일정 기간 캐시로 저장해둔다. 일반적으로 KT, LG, SK 등의 ISP DNS 서버를 사용한다.
 
### Root Name Server (Root DNS Server)

국제인터넷주소관리기구(ICANN)에서 직접 관리하는 서버로 인터넷상의 모든 TLD DNS 서버 IP 주소를 저장해두고 전 세계에 13개 만이 존재한다.

### Root DNS Mirror Server

기존 루트 DNS 서버를 복사한 것으로 미러 서버가 있는 국가는 외국의 루트 서버 없이 자체적으로 인터넷 통신을 관리할 수 있다.
 

### TLD Name Server (Top-Level-Domain DNS Server)
ICANN의 지사인 인터넷 할당 번호 관리기관(IANA)에서 관리하는 서버로 Authoritative Name Server의 주소를 저장해둔다.
 

### Authoritative Name Server (Authoritative DNS Server)
실제 도메인과 IP 주소를 매칭한 정보가 저장/변경되는 서버로 보통 가비아, 후이즈와 같은 도메인/호스팅 업체의 네임서버를 의미한다. 개인 DNS 서버를 구축한 경우에도 여기에 해당한다.

## DNS Query 방법

### 반복적 질의 (Iterative Query)

![!\[alt text\](../ETC/download.png)](<../ETC/Iterative Query.png>)

사용자가 Local DNS 서버에 query를 보내면 Local DNS 서버가 Root name 서버에 query를 보내 TLD 서버의 주소를 반환받고, 다시 TLD 서버에 query를 보낸다. 이렇게 최종 IP 주소를 받을 때까지 요청과 응답을 계속해서 Local DNS 서버가 반복하는 방법이다.

### 재귀적 질의 (Recursive Query)

![alt text](<../ETC/Iterative Query.png>)

사용자가 Local DNS 서버에 query를 보내면 Local DNS server가 Root name 서버에 query를 보내고, Root 서버는 자신의 서버에 없으면 해당 TLD 서버에 요청한다. 이렇게 재귀적으로 실제 도메인 정보를 가지고 있는 서버까지 query가 이동하여 IP 주소를 얻는 방법이다. 재귀적인 방법은 Root 서버에 너무 큰 부담을 준다는 단점이 있다.   


실제 DNS 서버는 반복과 재귀적인 방식을 함께 사용하며 Local DNS 서버에는 재귀, Root와 TLD 서버에는 반복, Authoritative 서버에는 재귀/반복적 query를 사용한다.

 