### [HTTP 프로토콜](https://youtu.be/TwsQX1AnWJU?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- 7계층 프로토콜
- 웹 표준 데이터(HTML, CSS, Javascript)를 웹 서버에게 요청하고 받아오는 프로토콜
- HyperText Transfer Protocol(하이퍼 텍스트 전송 프로토콜)
- www에서 쓰이는 핵심 프로토콜로 문서의 전송을 위해 쓰이며, 오늘날 거의 모든 웹 애플리케이션에서 사용되고 있다
- Request/Response(요청/응답) 동작에 기반하여 서비스 제공

### [HTTP 요청 프로토콜](https://youtu.be/rxaBwwI_JnI?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- HTTP Method 설명 중 GET, POST만 사용해야 한다고 하지만 개발자 입장에서 RESTful API 개발시 PUT, DELETE도 사용하는게 원칙임
- HTTP 요청 프로토콜의 구조   
![image](https://user-images.githubusercontent.com/28378553/125184753-5f144f80-e25b-11eb-90ee-0253ad964be5.png)
- Request line   
![image](https://user-images.githubusercontent.com/28378553/125184806-c16d5000-e25b-11eb-8431-e11342f9f06e.png)   
![image](https://user-images.githubusercontent.com/28378553/125184839-ea8de080-e25b-11eb-8fa0-7ae97c2c85fa.png)
- GET: URI에 요청 데이터를 포함시켜 보낸다
- POST: URI가 아닌 BODY에 요청 데이터를 보낸다

### [URL, URI란?](https://youtu.be/2ikhZ_fNP5Y?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- URI(Uniform Resource Identifier): 인터넷 상에서 특정 자원(파일)을 나타내는 유일한 주소
- URI의 구조   
![image](https://user-images.githubusercontent.com/28378553/125185008-0d6cc480-e25d-11eb-8f83-6c68c09f3767.png)

### [HTTP 요청 프로토콜 작성 실습](https://youtu.be/XbGJYsxed2w?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

### [URI 이해를 위한 실습](https://youtu.be/HBojczyd1Ac?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

### [HTTP 응답 프로토콜](https://youtu.be/kuucNF4Zvbs?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- HTTP 응답 프로토콜의 구조   
![image](https://user-images.githubusercontent.com/28378553/125185193-46f1ff80-e25e-11eb-9551-46438ddc8b4b.png)
- Status Line   
![image](https://user-images.githubusercontent.com/28378553/125185218-79036180-e25e-11eb-8bb1-4a67af2daa36.png)   
- 상태 코드   
![image](https://user-images.githubusercontent.com/28378553/125185222-8b7d9b00-e25e-11eb-905a-d972a2ef987a.png)   
  + 200-OK-Client의 요청이 성공했다는 것을 나타낸다
  + 403-Forbidden-Client가 권한이 없는 페이지를 요청했을 때
  + 404-Not Found-Client가 서버에 없는 페이지를 요청했을 때
  + 500-Internal Server Error-Server의 일부가 멈췄거나 설정 오류가 발생
  + 503-Service Unavailable-최대 Session 수를 초과했을 때

### [HTTP 헤더 포맷](https://youtu.be/mQTGmxendk8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
- 일반적인 정보를 담고 있는 일반 헤더   
![image](https://user-images.githubusercontent.com/28378553/125185308-25ddde80-e25f-11eb-8930-1ad825aa613a.png)
- 클라이언트 정보를 담고 있는 요청 헤더   
![image](https://user-images.githubusercontent.com/28378553/125185327-40b05300-e25f-11eb-9333-5667bd7099a5.png)
- 서버 정보를 담고 있는 응답 헤더   
![image](https://user-images.githubusercontent.com/28378553/125185373-72c1b500-e25f-11eb-85b5-0f8a65f0b8f0.png)

### [HTTP 프로토콜 분석 실습](https://youtu.be/dhMrKTwNI8U?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)
