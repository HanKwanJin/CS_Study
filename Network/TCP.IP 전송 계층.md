# TCP/IP 전송 계층

- 송신자와 수신자를 연결하는 통신 서비스 제공
- 연결 지향 데이터 스트림 지원, 신뢰성, 흐름 제어 제공
- 애플리케이션과 인터넷 계층 사이 데이터 전달의 중계 역할
- 대표적으로 TCP, UDP가 있다.
    - TCP (Transmission Control Protocol)
        - *패킷 사이 순서를 보장하고 연결지향 프로토콜을 사용해 연결하여 신뢰성을 구축해서 수신 여부를 확인하며 '가상회선 패킷 교환 방식' 사용
    - UDP (User Datagram Protocol)
        - 순서를 보장하지 않고 수신 여부를 확인하지 않으며, 단순히 데이터만 주는 '데이터그램 패킷 교환 방식' 사용
- 요약 : 데이터의 전달을 담당

*패킷 : 각 계층이 데이터를 프로토콜에 따라 처리하고 헤어들 추가한 데이터 단위

## 가상회선 패킷 교환 방식
각 패킷에 가상회선 식별자가 포함되며, 모든 패킷을 전송하면 가상회선이 해제되고 전송된 순서대로 도착한다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fod4Bz%2FbtrP3MyRXko%2FBAg2OqbnhQ0XEQ8caWsxgK%2Fimg.png)

위 그림을 보면 가상회선이 있고, 그 길을 따라 순서대로 이동하는 것을 볼 수 있다.

## 데이터그램 패킷 교환 방식
패킷이 독립적으로 이동하며 최적의 경로를 선택하여 간다.
하나의 메시지에서 분할된 여러개의 패킷은 서로 다른 경로로 전달될 수도 있으며 도착하는 순서가 정해져있지 않다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9969973359FEB59309)

위 그림을 보면 패킷이 독립적으로 해당 패킷의 최적의 경로를 선택하여 가고, 도착하는 순서가 '다를 수도' 있다는 것을 볼 수 있다.