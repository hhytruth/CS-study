### [UDP 프로토콜](https://youtu.be/3MkI3FBFzX8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- 사용자 데이터그램 프로토콜(User Datagram Protocol)
- UDP의 전송 방식은 너무 단순해서 서비스의 신뢰성이 낮고, 데이터그램 도착 순서가 바뀌거나, 중복되거나, 심지어는 통보 없이 누락시키기도 한다
- 일반적으로 오류의 검사와 수정이 필요 없는 프로그램에서 수행할 것으로 가정한다
- 안전한 연결을 지향하지 않는다   
![image](https://user-images.githubusercontent.com/28378553/125183395-5585ea00-e251-11eb-95dd-ec842bc594b2.png)    
Length: Header+Payload 길이
- UDP 프로토콜을 사용하는 프로그램
  + 도메인을 물으면 IP를 알려주는 DNS 서버
  + UDP로 파일을 공유하는 tftp 서버
  + 라우팅 정보를 공유하는 RIP 프로토콜

### [tftpd로 파일 전송 실습](https://youtu.be/5Woau-EJChw?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
