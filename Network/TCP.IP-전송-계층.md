# TCP/IP 전송 계층

- 송신자와 수신자를 연결하는 통신 서비스 제공
- 연결 지향 데이터 스트림 지원, 신뢰성, 흐름 제어 제공
- 애플리케이션과 인터넷 계층 사이 데이터 전달의 중계 역할
- 대표적으로 TCP, UDP가 있다.
    - TCP (Transmission Control Protocol)
        - 패킷[1] 사이 순서를 보장하고 연결지향 프로토콜을 사용해 연결하여 신뢰성을 구축해서 수신 여부를 확인하며 '가상회선 패킷 교환 방식' 사용
    - UDP (User Datagram Protocol)
        - 순서를 보장하지 않고 수신 여부를 확인하지 않으며, 단순히 데이터만 주는 '데이터그램 패킷 교환 방식' 사용
- 요약 : 데이터의 전달을 담당

---
[1] 패킷 : 각 계층이 데이터를 프로토콜에 따라 처리하고 헤어들 추가한 데이터 단위

## 가상회선 패킷 교환 방식
각 패킷에 가상회선 식별자가 포함되며, 모든 패킷을 전송하면 가상회선이 해제되고 전송된 순서대로 도착한다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fod4Bz%2FbtrP3MyRXko%2FBAg2OqbnhQ0XEQ8caWsxgK%2Fimg.png)

위 그림을 보면 가상회선이 있고, 그 길을 따라 순서대로 이동하는 것을 볼 수 있다.

## 데이터그램 패킷 교환 방식
패킷이 독립적으로 이동하며 최적의 경로를 선택하여 간다.
하나의 메시지에서 분할된 여러개의 패킷은 서로 다른 경로로 전달될 수도 있으며 도착하는 순서가 정해져있지 않다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9969973359FEB59309)

위 그림을 보면 패킷이 독립적으로 해당 패킷의 최적의 경로를 선택하여 가고, 도착하는 순서가 '다를 수도' 있다는 것을 볼 수 있다.

## TCP 연결 성립 과정
TCP는 신뢰성을 확보할 때 '3-way handshake'라는 작업을 진행한다.
이 작업으로 신뢰성이 구축되고, 데이터를 전송한다. UDP는 이 과정이 없어 신뢰성이 없는 계층이라 불린다.

![image](https://goodgid.github.io/assets/img/network/tcp_ip_3way_4way_1.png)

### SYN[2] 단게 (#1)
클라이언트는 서버에 ISN[3]을 담아 SYN을 보낸다. ISN은 새로운 TCP연결의 첫 번째 패킷에 할당된 임의의 시퀀스 번호이다. (장치마다 다를 수 있음)
### SYN + ACK[4] 단계 (#2)
서버는 클라이언트에 SYN을 수신하고 서버의 ISN을 보내며 승인번호로 클라이언트의 ISN+1을 반환
### ASK 단계 (#3)
클라이언트가 서버에서 반환한 ISN+1 한 값(승인번호)을 담아 ACK를 서버에 보냄

---
[2] SYN : SYNchronization - 연결 요청 플래그, 다른 컴퓨터로 전송된 TCP패킷으로 연결이 이루어 지도록 요청
[3] ACK : ACKnowledgement - 응답 플래그, 다른 컴퓨터나 네트워크 장치가 다른 컴퓨터에 SYN/ACK 또는 다른 요청을 보낸 것을 확인한 응답
[4] ISN : Initial Sequence Numbers - 초기 네트워크 연결을 할 때 할당된 32비트 고유 시퀀스 번호

## TCP 연결 해제 과정
TCP가 연결을 해제할 때는 4-way handshake 과정을 거침

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtQR1l%2FbtqyJRYdm3E%2F143elB5WCHDlofiAsax2J1%2Fimg.png)

### FIN_WAIT_1
먼저 클라이언트가 연결을 닫으려 할 때 FIN으로 설정된 세그먼트[5]를 보냄. 그리고 클라이언트는 FIN-WAIT-1 상태로 들어가고 서버의 응답 대기
### CLOSE_WAIT
서버는 클라이언트로 ACK라는 승인 세그먼트를 전송. 이후 CLOSE-WAIT 상태로 전환하고 클라이언트가 전송을 받으면 FIN-WAIT-2로 전환
### LAST_ACK
서버가 ACK를 보내고 일정 시간 이후 클라이언트에 FIN이라는 세그먼트 전송
### TIME_WAIT[6]
클라이언트가 TIME_WAIT 상태가 되고 다시 서버로 ACK를 전송하여 서버는 CLOSED 상태가 됨. 이후 어느 정도의 시간을 대기하면 연결이 닫히고, 클라이언트와 서버의 모든 자원 연결 해제

[TIME_WAIT] 일정 시간이 지나고 연결을 닫는 이유
1. 지연된 패킷이 발생할 경우를 대비
    - 패킷이 늦게 도달하고 이를 처리하지 못하면 데이터 무결성[7] 문제 발생(일부 데이터만 들어오는 현상)
2. 두 장치 연결이 닫혔는지 확인
    - server의 LAST_ACK 상태에서 ACK를 클라이언트에게서 받으면 CLOSE 상태로 들어가는데, 어떤 문제로 LAST_ACK 상태에서 닫히면 새로운 연결을 하려고 할 때, 장치는 계속 LAST_ACK로 되어있기 때문에 오류가 발생한다.
 
---
[5] Segment : TCP로 연결된 세션간의 전달되는 데이터 단위
[6] TIME_WAIT : 소켓이 바로 소멸되지 않고 일정 시간 유지되는 상태
[7] 데이터 무결성(data integrity) : 데이터의 정확성과 일관성을 유지하고 보증하는 것