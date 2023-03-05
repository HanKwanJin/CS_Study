# HTTP3란?

<img src="https://user-images.githubusercontent.com/28129081/56917902-a4735900-6af7-11e9-8617-3dc7547eda7a.JPG">

HTTP/3은 TCP를 기반으로 한 HTTP/2와 다르게 QUIC이라는 계층 위에서 돌아가며, TCP 기반이 아닌 UDP 기반으로 돌아갑니다. 또한, HTTP/2에서 장점이었던 멀티플렉싱을 가지고 있으며 초기 연결 설정 시 지연 시간 감소라는 장점이 있습니다.

# QUIC란?

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVaGm6%2FbtqB3qH57Fa%2FO0TgWavUQk1EnKFWbDrkkK%2Fimg.png">

<img src="https://lh3.googleusercontent.com/o62Ohn1Ppxna6zz0NtavqRyetjryOj-81Sz4bRt3U8lURVblk5RKOaCcf57i6BkmprremePJpq_sQcxfJiuA4wJBmRp3pR4BS1P-yiT6UNUPvnBeP_rLz9bvHxFE15kuNBM2hpE">

HTTP/3에서는 QUIC 위에서 돌아간다고 하였는데요. QUIC의 장점은 어떤 것들이 있는지 알아보겠습니다.

## QUIC 장점

- 암호화가 프로토콜의 일부기능으로 포함되어 있습니다.

- 스트림 연결과 암호화 스펙등을 포함한 모든 핸드쉐이크 단일 요청/응답으로 끝납니다.

- 패킷이 개별적으로 암호화되며, 다른 데이터 부분의 패킷을 기다릴 필요가 없습니다.

- 통신이 멀티플렉싱 되며 이를 통해 HOL Blocking을 해결합니다.

- QUIC는 운영체제 커널과 독립적으로 응용 프로그램 공간 내에서 구현할 수 있으며, 덕분에 데이터의 이동에 따른 컨텍스트 전환에 의한 오버헤드가 없어집니다.

- Source Address와 상관없이 서버에 대한 연결을 고유하게 식별하는 연결 식별자가 포함되어 있어, IP 주소가 변경되더라도 커넥션을 유지할 수 있습니다.

- 순방향 오류 수정 매커니즘(FEC, Forward Error Correction)이 적용되어 있어서 전송한 패킷이 손실되었다면 수신 측에서 에러를 검출하고 수정하는 방식으로 열악한 네트워크 환경에서도 낮은 패킷 손실률을 자랑합니다.

