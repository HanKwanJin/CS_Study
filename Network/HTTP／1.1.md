## HTTP/1.0과 HTTP/1.1이 다른점
<br>

<img src="https://user-images.githubusercontent.com/49395754/221134435-086eaeb1-31cb-46d7-b127-f26740ef186d.png" width="500" height="300">


1. 커넥션 유지(Persistent Connection) <br>
HTTP/1.0에 제일 큰 단점이라고 하면 nonPersistent라는 점이다. 하지만 HTTP1.1부터는 다르다. 
   *  요청 헤더 connection:keep-alive 속성으로 지속적 연결 상태(persistent connection)을 유지한다.
   * 요청을 할 때마다 연결하지 않고 기존의 연결을 재사용하는 방식으로 HTTP/1.1부터는 지속적 연결 상태가 기본이고 해제하기 위해서는 명시적으로 요청 헤더를 수정해야 한다.
2. 파이프라이닝(Pipelining)
   * 파이프 라이닝이 존재하지 않을 때는 HTTP 요청이 순차적으로 이루어진다.
   * 파이프 라이닝이 생긴 이후 부터는 동시에 요청하고 이에 대해 각각 응답을 받아 처리한다.
3. 호스트 헤더 (Host Header)
   * HTTP 1.0 환경에서는 하나의 IP에 여러 개의 도메인을 운영할 수 없다. 도메인 마다 IP를 구분해서 준비해야 한다. 도메인만큼 서버의 개수도 늘어날 수 밖에 없는 구조이다. 
   * HTTP 1.1 에서 Host 헤더의 추가를 통해 비로소 버츄얼 호스팅이 가능해졌다. 
4. 강력한 인증 절차 (Improved Authentication Procedure)
   * proxy-authentication
   * proxy-authorization <br>
   HTTP 1.1에 추가된 헤더이다. 이것은 클라이언트와 서버 사이에 프록시가 위치한 경우 프록시가 사용자의 인증을 요구할 수 있다.


<br>

## HTTP/1.1의 단점 
  
  ### HOL(Head of Line) blocking: 특정 응답의 지연
  <img src="https://user-images.githubusercontent.com/49395754/221137414-d536b232-3bf5-4dce-8dbf-b7f0fa66ade4.png" width="300" height="300">
  <br>
  네트워크에서 같은 큐에 있는 패킷이 그 첫 번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상이다. 

  <br>

  * 예를 들면 식당에가서 제일 먼저 돈까스를 시킨후에 라면, 콜라를 시켰다.
  * 근데 돈까스가 나올 때 까지 라면과 콜라를 주지 않는 것이다.  
  * 더 큰 문제는 만약 돈까스 재료가 부족해 가계에서 돈까스 재료를 사러가야 한다.
  * 하지만 재료가 도착해 돈까스를 만들 때 까지 라면과 콜라를 주지 않는다.
  * 그럼 배고픈 학생들이 화가 난다.
  * 이게 HOL blocking이다.

  <br>

  ### 왜 순서대로 응답을 줘야 할까?
   웹 서버는 Pipelining 을 통해 한번에 여러 개의 요청을 받을 수 있으나, 응답 순서는 요청 순에 따라야 함이 HTTP 프로토콜의 규칙이 존재한다!!

  <br>

  ### 무거운 헤더 구조
  HTTP/1.1의 헤더에는 많은 메타 정보들이 저장되어 있다. 클라이언트가 서버로 보내는 HTTP 요청은 매 요청 때마다 중복된 헤더 값을 전송하게 되며 서버 도메인에 관련된 쿠키 정보도 헤더에 함께 포함되어 전송된다. 이러한 반복적인 헤더 전송, 쿠키 정보로 인한 헤더 크기 증가가 HTTP/1.1의 단점이다.