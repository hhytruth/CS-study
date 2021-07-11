### [TCP 프로토콜](https://youtu.be/cOK_f9_k_O0?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- 전송 제어 프로토콜(Transmission Control Protocol)은 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 통신을 안정적으로, 순서대로, 에러없이 교환할 수 있게 한다
- UDP보다 안전하지만 느리다
- 안전한 연결을 지향한다   
![image](https://user-images.githubusercontent.com/28378553/125183584-9c281400-e252-11eb-875f-984e7b651675.png)   
Offset: 헤더의 길이/4   
Window: 얼만큼 더 데이터를 받을지 상대방에게 알려주는 부분

### TCP 플래그
- U: Urgent flag, 긴급 비트, 우선순위가 높다고 표시
- A: ACK flag, 승인 비트
- P: Push flag, 밀어넣기 비트
- R: Reset flag, 초기화 비트
- S: Sync flag, 동기화 비트, 상대방과 연결을 시작할 때 무조건 사용하는 플래그, 서로 상태를 동기화
- F: Fin flag, 종료 비트, 연결을 끊음

### [TCP 3Way Handshake](https://youtu.be/Ah4-MWISel8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- TCP를 이용한 통신 과정
  + 연결 수립 과정: 가장 먼저 수행되는 과정
    1. 클라이언트가 서버에게 요청 패킷을 보내고
    2. 서버가 클라이언트의 요청을 받아들이는 패킷을 보내고
    3. 클라이언트는 이를 최종적으로 수락하는 패킷을 보낸다
  + 위의 3개와 과정을 3Way Handshake라고 부른다   
![image](https://user-images.githubusercontent.com/28378553/125183954-2f624900-e255-11eb-8f38-f8eb298648dc.png)

### [TCP를 이용한 데이터 전송 과정](https://youtu.be/0vBR666GZ5o?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
1. 보낸 쪽에서 또 보낼 때는 SEQ 번호와 ACK 번호가 그대로다
2. 받는 쪽에서 SEQ 번호는 받은 ACK 번호가 된다
3. 받는 쪽에서 ACK 번호는 받은 SEQ 번호+데이터의 크기   
![image](https://user-images.githubusercontent.com/28378553/125184101-127a4580-e256-11eb-9700-fa6c87354a33.png)

### [TCP의 연결 상태 변화](https://youtu.be/yY0uQf0BTH8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)   
![image](https://user-images.githubusercontent.com/28378553/125184198-afd57980-e256-11eb-9a50-3abd62b3614d.png)   
ESTABLISHED: 연결이 수립된 상태   
LISTEN: 포트를 열어놓고 요청이 오는지 계속 듣고 있는 상태   
![image](https://user-images.githubusercontent.com/28378553/125184260-443fdc00-e257-11eb-817b-dcc187238b05.png)

### [TCP 프로토콜 분석 실습](https://youtu.be/WseqBDo-j3Y?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
