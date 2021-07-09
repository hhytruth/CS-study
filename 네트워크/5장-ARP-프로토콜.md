### [ARP 프로토콜](https://youtu.be/LDsp-Xb168E?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- ARP 프로토콜은 같은 네트워크 대역에서 통신을 하기 위해 필요한 MAC주소를 IP주소를 이용해서 알아오는 프로토콜이다
- ARP 프로토콜의 구조   
![image](https://user-images.githubusercontent.com/28378553/125107444-cdea8f00-e11b-11eb-9bb8-d79ffdda3921.png)   
Opcode: 요청을 하는지(0001), 요청에 응답하는지(0002) 표시

### ARP 프로토콜의 통신 과정
1. ARP 프로토콜 작성시, 요청을 보낼 때는 아직 목적지의 MAC주소를 알 수 없기 때문에 00 00 00 00 00 00으로 작성하여 보내게 된다. 목적지의 IP주소는 작성한다.
2. 이더넷 프로토콜에서는 FF FF FF FF FF FF로 작성하게 보낸다.(FF FF FF FF FF FF는 브로드캐스트를 의미하기 때문에 같은 네트워크의 전 기기로 전송된다.)
3. 전 기기는 디캡슐레이션 과정에서 ARP 프로토콜을 확인한다. 이 때 목적지 IP주소가 일치하지 않을 경우 패킷을 버린다.
4. 목적지 IP주소가 일치한 기기는 응답 프로토콜에 본인의 MAC주소를 작성하여 보내준다. 이 때 이더넷 프로토콜에서는 브로드 캐스트를 하지 않고 목적지의 정확한 MAC 주소를 작성할 수 있게 된다.(보낸 이를 알기 때문에)
5. 결과적으로 요청을 보낸 기기가 응답을 보낸 기기의 MAC주소를 알게 되고, 이를 ARP 캐시 테이블이라는 곳에 저장해두고 활용한다.(휘발적)

### ARP 테이블
- 통신했던 컴퓨터들의 주소는 ARP 테이블에 남는다

### [ARP 프로토콜 실습](https://youtu.be/-M_S50Ga384?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
