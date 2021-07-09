### [IPv4 프로토콜](https://youtu.be/_i8O_o2ozlE?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- 네트워크 상에서 데이터를 교환하기 위한 프로토콜
- 데이터가 정확하게 전달될 것을 보장하지 않는다
- 중복된 패킷을 전달하거나 패킷의 순서를 잘못 전달할 가능성도 있다
- 데이터의 정확하고 순차적인 전달은 그보다 상위 프로토콜인 TCP에서 보장한다
- IPv4 프로토콜의 구조(20바이트)   
![image](https://user-images.githubusercontent.com/28378553/125110289-59195400-e11f-11eb-88ab-887a4b1c61d8.png)    
IHL=20~60/4   
Identification: 보낼 때 나뉘어진 데이터를 다시 하나로 합칠 때 어떤 데이터를 합쳐야 할 지 구분짓는 아이디     
IP Flags-x: 안 씀   
IP Flags-D: 데이터를 쪼개지 않고 통째로 보내겠다고 명시(거의 안 씀)   
IP Flags-M(More fragments): 조각화가 되어있을 때 뒤에 더 패킷이 있다는 것을 명시(최대 단위보다 크기가 클 때 1)   
Fragment Offset: 쪼개진 데이터의 순서를 알아볼 수 있게 offset(시작으로부터 얼만큼 떨어져있는지)    
Protocol: 상위 프로토콜

### [ICMP 프로토콜](https://youtu.be/JaBCIUsFE74?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- Internet Control Message Protocol: 네트워크 컴퓨터 위에서 돌아가는 운영체제에서 오류 메시지를 전송받는 데 주로 쓰인다
- 프로토콜 구조의 Type과 Code를 통해 오류 메시지를 전송받는다
- ICMP 프로토콜의 구조   
![image](https://user-images.githubusercontent.com/28378553/125112544-47857b80-e122-11eb-84a3-56fdd08a39b2.png)
  + Type: 대분류
    + 8: 요청, 0: 응답
    + 3: destination unreachable, 11: time exceeded
    + 5: ICMP Redirect(보안)
  + Code: 소분류

### [IPv4, ICMP프로토콜 실습](https://youtu.be/8ZwTvTuZlVw?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

### [라우팅 테이블](https://youtu.be/CjnKNIyREHA?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- 패킷을 어디로 보내야 하는지 설정되어 있는 라우팅 테이블
- 다른 네트워크와 통신 과정
1. 다른 대역의 A와 B가 통신할 때를 가정해보자.
2. A의 자신이 라우팅 테이블에 B의 네트워크 대역이 존재해야 통신이 가능하다.
3. A는 요청하는 프로토콜을 작성해서 보낸다.(ICMP: type 8, 요청으로 작성/IPv4/Eth: 목적지 맥주소는 가까운 곳에서 갈 수 있는 곳까지만 작성. 즉 게이트웨이 맥주소를 작성. 만약 게이트웨이의 맥주소도 알 수 없을 경우 ARP 프로토콜을 통해 알아오게 된다.)
4. 공유기는 이를 전송받아 자신의 라우팅 테이블을 확인한다. 그 후 Eth 프로토콜의 내용을 자신에게 가까운 대역에 전송되도록 바꿔서 다시 작성한다.
5. 이런 작업이 반복되다가 상대방의 게이트웨이까지 도착하고, 해당 게이트웨이도 다시 Eth 프로토콜을 다시 작성해 B로 보내주게 된다.
6. B는 응답하는 프로토콜을 작성해서 보낸다.(ICMP: type 0, 응답)

### [라우팅 테이블 확인 실습](https://youtu.be/tVntagSJctc?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

### [IPv4 조각화 이론](https://youtu.be/_AONcID7Sc8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- 조각화란?
  + 큰 IP 패킷들이 적은 MTU(Maximum Transmission Unit)를 갖는 링크를 통하여 전송되려면 여러 개의 작은 패킷으로 쪼개어/조각화되어 전송돼야 한다. 즉, 목적지까지 패킷을 전달하는 과정에 통과하는 각 라우터마다 전송에 적합한 프레임으로 변환이 필요하다.
  + 일단 조각화되면, 최종 목적지에 도달할 때까지 재조립되지 않는 것이 일반적이다.   
  ![image](https://user-images.githubusercontent.com/28378553/125116111-2ecb9480-e127-11eb-8d2e-1939dd081047.png)   
  Offset: 8로 나눔
- 큰 데이터를 보낼 때 패킷이 조각화하는 과정   
![image](https://user-images.githubusercontent.com/28378553/125116418-a7caec00-e127-11eb-89da-12eb7586e8ac.png)

### [IPv4 조각화 실습](https://youtu.be/QKEL9aBgHtg?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
