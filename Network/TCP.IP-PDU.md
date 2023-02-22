# PDU (Protocol Data Unit)

***네트워크의 어떠한 계층에서 계층으로 데이터가 전달될 때, 한 덩어리의 단위를 PDU라고 한다.***
- 데이터 통신에서 상위 계층이 전달한 데이터에 붙이는 제어 정보
- PDU는 제어 관련 정보들이 포함된 '헤더(header)', 데이터를 의미하는 'pay load'로 구성되어 있는데 계층마다 부르는 이름이 다르다.
    - 애플리케이션 계층 : 메시지 - 데이터라고도 한다고 함.
    - 전송 계층 : 세그먼트(TCP), 데이터그램(UDP)
    - 인터넷 계층 : 패킷(IP)
    - 링크 계층 : 프레임(데이터 링크 계층), 비트(물리 계층)

![image](https://mblogthumb-phinf.pstatic.net/MjAxODA2MTJfMTU2/MDAxNTI4Nzk0MDEyMjAx.bXwOTui01WflROmaw2OMeYBYh9JOV4ngtmhijFh4miYg.1nnMrBZVMFeEUv-DSZEX6gjgE3OZh8nN_9Wg0ZALB5Ug.PNG.yeopil-yoon/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-12_%EC%98%A4%ED%9B%84_5.59.41.png?type=w800)
<br>
**위 그림에서 data는 message와 같다.**

## PDU 구성
- SDU(Service Data Unit) : 전송하려는 데이터
- PCI(Protocol Control Information) : 제어 정보, 송신자와 수신자 주소나 오류코드 제어 정보 등이 있음. (데이터에 제어 정보를 붙이는 것을 캡슐화라고 함)
```
SDU + PCI = PDU
```

## 참고
- PDU 중 아래 계층인 비트로 송수신하는 것이 모든 PDU 중 가장 빠르고 효율성이 높다.
    - 하지만 애플리케이션 계층에선 문자열을 기반으로 송수신을 하는데, 그 이유는 헤더에 authorization 값 등 다른 값들을 넣는 확장이 쉽기 때문이다.
---
### 이미지 출처
https://m.blog.naver.com/yeopil-yoon/221315395527


