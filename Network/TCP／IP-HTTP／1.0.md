## HTTP란?
<br>

* HTTP(Hyper Text Transfer Protocol)는 인터넷에서 주로 사용하는 데이터를 송수신하기 위한 프로토콜이다. 
* 애플리케이션 계층으로서 웹 서비스 통신에 사용된다.

<br>

## HTTP/1.0이란?

<img src="https://user-images.githubusercontent.com/49395754/220665803-69a14182-c62f-48db-a0e0-55b93a16bf6d.png" width="300" height="300">
<br>


* HTTP/1.0 은 기본적으로 한 연결당 하나의 요청을 처리하도록 설계되었다. 즉, TCP 세션을 지속적으로 유지할 수가 없다.
* HTTP/1.0은 매번 데이터를 요청하고 수신할 때마다 새로운 TCP 세션을 맺어야 한다. 
* HTTP/1.0은 Non-persistent HTTP이다.
* 1996년에 만들어졌다.

<br>

## HTTP/1.0의 단점

### RTT 증가

서버로부터 파일을 가져올 때마다 TCP의 3-웨이 핸드셰이크를 계속해서 열어야 하기 때문에 RTT가 증가한다.

<br>

## RTT 증가 해결방법

매번 연결할 때마다 RTT가 증가하니 서버에 부담이 많이 가고 사용자 응답 시간이 길어졌다. 이를 해결하기 위해 이미지 스플리팅, 코드 압축, 이미지 Base64 인코딩을 사용한다.

<br>

### 이미지 스프라이트

많은 이미지를 한번에 다운로드 받게 되면 과부하가 걸리기 때문에 많은 이미지가 합쳐 있는 하나의 이미지를 다운로드 받고, 이를 기반으로 background-image의 position을 이용하여 이미지를 표기하는 방법이다.

* 책에는 이미지 스플리팅이라고 하지만 요즘 이미지 스프라이트라고 부른다고 한다.

* 웹의 경우에서는 "여러 개의 이미지를 하나의 이미지로 만들어 놓는 것"을 의미한다.


<img src="https://user-images.githubusercontent.com/49395754/220670161-5e75c104-6551-436a-8258-807e0c1e9da8.png" width="400" height="300">

이렇게 4개의 아이콘을 하나로 합쳐서 다운 받는 것이다.

```
<a href="#" class="naver">네이버</a>
<a href="#" class="fb">페이스북</a>
<a href="#" class="google">구글</a>
<a href="#" class="kakao">카카오</a>
```
```
a::after {
      content: "";
      display: block;
      width: 28px;
      height: 28px;
      background-image: url(./asset/images/css_sprites.png);
}

.naver::after {
      background-position: -58px -58px;
    }

    .fb::after {
      background-position: -10px -10px;
    }

    .google::after {
      background-position: -58px -10px;
    }

    .kakao::after {
      background-position: -10px -58px;
    }
```
이렇게 background를 이용해 4개를 합쳐서 가져온다.
<br>
출처 : https://velog.io/@untiring_dev/HTMLCSS-Day31.-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EC%8A%A4%ED%94%84%EB%9D%BC%EC%9D%B4%ED%8A%B8-%EA%B8%B0%EB%B2%95

<br>

### 코드 압축

코드 압축은 코드를 압축해서 개행 문자, 빈칸을 없애서 코드의 크기를 최소화하는 방법이다.<br>
책에서의 예시를 보면 모든 코드의 띄어쓰기와 개행문자를 없에고 ,로 대체한다.

### 이미지 Base64 인코딩
* 이미지 파일을 64진법으로 이루어진 문자열로 인코딩하는 방법이다. <br>
* 이 방법을 사용하면 서버와의 연결을 열고 이미지에 대해 서버에 HTTP 요청을 할 필요가 없다는 장점이 있다. <br>
* 하지만 Base64 문자열로 변환할 경우 37% 정도 크기가 더 커지는 단점이 있다.
* 이런 단점에도 사용하는 이유는 Base64는 모든 가능한 바이트값을 신뢰할 수없는 통신 채널을 통해 바이너리 데이터를 안전하게 전송할 수 있게 하는 것이다. 
* Base64는 어떤 문자와 기호를 쓰느냐에 따라 다양한 변종이 있지만, 대부분 처음 62개는 알파벳 A-Z, a-z와 0-9를 사용하며 마지막 두 개를 어떤 기호를 쓰느냐의 차이만 있습니다.
![image](https://user-images.githubusercontent.com/49395754/220673455-7e6877a0-963d-41b8-aaef-83a330d47449.png)
인코딩을 하는 과정을 보여주는 예시이다.