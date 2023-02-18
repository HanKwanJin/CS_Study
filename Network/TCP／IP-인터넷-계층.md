## TCP/IP 인터넷 계층

* 인터넷 계층은 장치로부터 받은 네트워크 패킷을 IP 주소로 지정된 목적지로 전송하기 위해 사용되는 계층이다.
* IP, ARP, ICMP 등이 있으며 패킷을 수신해야 할 상대의 주소를 지정하여 데이터를 전달한다.
* 상대방이 제대로 받았는지에 대해 보장하지 않는 비연결형적인 특징을 가지고 있다.

## IP 

### IPv4 패킷의 구조

<img src="https://user-images.githubusercontent.com/49395754/219856585-7f0f5050-c2e2-49b7-9a98-9e3be4fdcdd1.png" width="500" height="300">
<br>

1. VER (4bits) : IP의 version을 나타낸다.
2. HLEN 혹은 IHL (4bits) :  IP헤더의 크기를 나타낸다.
3. TOS (Type of Service) (8bits) : 요구되는 서비스 타입이다.
4. Total Length (16bits) : IP헤더와 데이터를 포함한 IP패킷의 크기를 나타낸다.
5. Identification 혹은 Fragment Identification (16bits) :  데이터링크의 MTU size에 따라 조각화된 패킷을 복원하기 위한 식별자이다
6. Flags 혹은 Fragmentation Flags (3bits) : 
    + 첫번째 bit는 무조건 0
    + 두번째 bit는 DF(Don't Fragment) bit로 이 값이 1이면 패킷을 조각화 하지 않는다.
    + 마지막 bit는 MF(More Fragment) bit로 분활된 패킷이 마지막일 경우 0 이고 추가로 더 있을 경우는 1이다.
7. FO (Fragmentation Offset) (13bits) : 분할된 Fragment가 원래 데이터에서 어떤 위치였는지 나타내는 값으로 단위는 8-byte(8옥텟)이다. 
8. TTL(Time to live) (8bits) :  패킷이 네트워크 상에 얼마나 오래 살아남을 수 있는지를 알려주는 값이다.
9. Protocol (8bits) : 다음 상위계층(전송계층)의 프로토콜이 무엇인지 나타낸다.
10. Header checksum (16bits) : IP헤더가 손상되지 않았다는 것을 보증하기 위한 checksum이다. 
11. Source IP address (32bits) : 출발지 IP주소이다.
12. Destination IP address (32bits) : 목적지 IP 주소이다.
13. Options (0~40bytes) : 가변길이를 갖는 옵션 값은, 일반적으로는 사용되지 않고 테스트나 디버그 등의 용도로 사용된다.
    * 단일 바이트 옵션
       + 옵션 종료(end of option)
       + 무 동작(no operation)
    * 다중 바이트 옵션
       + 경로 기록 옵션 (record route)
       + 엄격한 발신지 경로 옵션 (strict source route)
       + 느슨한 발신지 경로 옵션 (loose source route)
       + 타임스탬프 (Timestamp)

<br>

## ARP

### ARP 패킷 구조

<img src="https://user-images.githubusercontent.com/49395754/219857420-368d075f-5d11-4fa8-8360-fad9b670d32e.png" width="400" height="300">

<Br>
ARP는 Address Resolution Protocol의 약자로 IP 주소를 MAC 주소와 매칭 시키기 위한 프로토콜입니다.

어떤 호스트나 라우터가 다른 호스타나 라우터에 보낼 IP 데이터그램을 가지고 있다면 송신자는 수신자의 논리 주소인 IP 주소를 가지고 있다. 그러나 IP 데이터그램은 물리적인 네트워크를 통과하기 위해 프레임 내에 캡슐화되어야 한다. <br>
즉, 송신자는 수신자의 물리 주소(MAC)를 알아야 한다. <br>
ARP는 IP 프로토콜로부터 논리 주소를 받아 이를 해당하는 물리 주소로 변환한 후 데이터링크 계층에 전달한다!!!

* ARP 요청은 브로드캐스트로 모든 곳에 요청하지만 응답은 유니캐스트로 목적지와 출발지만 소통한다.

<br>

## ICMP

<img src="https://user-images.githubusercontent.com/49395754/219864217-0a3bf651-e4e7-4195-a4d4-2d9a3ad8aa5d.png" width="400" height="300">

인터넷 제어 메시지 프로토콜이라고 한다.
이것은 네트워크 내 장치가 데이터 전송과 관련된 문제를 전달하기 위해 사용하는 프로토콜이다.

### ICMP가 필요한 이유

IP 프로토콜은 TCP 처럼 흐름 제어와 혼잡 제어 메커니즘이없다. 하지만 호스트는 간혹 라우터나 다른 호스트가 동작하고 있는지 알 필요가 있다. 이 단점을 보완하고자 ICMP가 생겼다.

### ICMP의 용도

인터넷 제어 메시지 프로토콜(ICMP)는 오류 보고 및 네트워크 진단 수행에 사용됩니다. 오류 보고 프로세스에서 ICMP는 데이터가 제대로 오지 않을 때 수신자에서 발신자에게 메시지를 보냅니다. 진단 프로세스 내에서 ICMP는 데이터 전송 방법에 대한 정보를 제공하기 위해 핑 및 트레이스라우트에서 사용하는 메시지를 보내는 데 사용됩니다.

* 오류 보고 메시지 (Error-reporting messages)
  + 목적지 도달 불가 (Destination unreachable) : 라우터가 데이터그램을 전달할 수 없거나 호스트가 데이터그램을 배달 수 없을 때 라우터나 호스트는 데이터그램을 시작했던 발신지 호스트에게 목적지 도달 불가 메시지를 낸다.
  + 발신지 억제 (Source quench) : 라우터나 목적지 호스트에서 혼잡으로 인해 데이터그램이 폐기되었음을 발신지에게 알린다.
  + 시간 경과 (Time exceeded) : 수명 필드를 감소한 후 이 값이 0이 되면 발생, 정해진 시간 내에 모든 단편을 받지 못했으면 이미 수신된 단편을 폐기하고 메시지 발생
  + 매개변수 문제 (Parameter Problem) : 목적지 호스트가 데이터그램의 필드에서 불명확하거나 빠진 값을 발견하게 되면 발생
  + 재지정 (Redirection) : 쉽게 말하면 목적지 까지 더 빠른 길을 찾기 위한 오류 보고 메시지이다. 

* 질의 메시지 (Query Message)
  + 에코 요청과 응답 (echo request and reply) : 호스트와 라우터가 서로 통신할 수 있는지 결정할 때 사용한다.
  + 타임스탬프 요청과 응답 (timestamp request and reply) : IP 데이터그램이 둘 사이를 지나가는 데 필요한 왕복 시간을 결정할 수 있다.
