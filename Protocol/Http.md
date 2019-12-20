#### Conception
HyperText Transfer Protocol.  
클라이언트와 서버 사이에서 이루어지는 요청/응답 프로토콜.  
- stateless protocol  
각각의 데이터 요청은 독립적이다. 이전 요청과 다음 요청은 서로 관련이 없다.  
이 특징 덕에 서버는 세션 등 추가 정보를 관리하지 않아도 된다.  

#### Request Methods  
HTTP Verbs 라고도 부르며, 데이터에 대해 특정 action을 수행하고 싶을 때 사용.  
GET : 존재하는 자원에 대한 요청  
POST : 새로운 자원을 생성  
PUT : 존재하는 자원에 대한 변경  
DELETE : 존재하는 자원에 대한 삭제  
HEAD : 서버 헤더 정보를 획득. GET과 비슷하나 Response Body를 반환하지 않음.  
OPTIONS : 서버 옵션들을 확인하기 위한 요청.  

#### Request Structure  
1. Start line  
- HTTP Method : 해당 요청이 의도한 action을 정의.  
- Request Target: 해당 request가 전송되는 endpoint target.  
- HTTP Version: http 버전.  
> GET / search HTTP/ 1.1  

2. Header  
요청 정보를 담는다.  
Host : 요청이 전송되는 target의 host Url.  
User-Agent : 요청을 보내는 클라이언트의 정보. ex. 웹브라우저에 대한 정보.  
Accept : 해당 요청이 받을 수 있는 응답 타입.  
Connection : 해당 요청이 끝난 후, 클라이언트와 서버 간 네트워크 커넥션 유지 여부에 대해 지시.  
Content type : 해당 요청이 보내는 메세지 body type. JSON을 보내면 application/json.  
Content length : 메세지 body의 길이.  

> Accept: */*
  Accept-Encoding: gzip, deflate
  Connection: keep-alive
  Content-Type: application/json
  Content-Length: 257
  Host: google.com
  User-Agent: HTTPie/0.9.3  

3. Body  
요청의 실제 내용. Get Request들은 Body가 없는 경우가 많다.  
> POST /payment-sync HTTP/1.1  
  Accept: application/json  
  Accept-Encoding: gzip, deflate  
  Connection: keep-alive  
  Content-Length: 83  
  Content-Type: application/json  
  Host: intropython.com  
  User-Agent: HTTPie/0.9.3  
  {  
    "imp_uid": "imp_1234567890",  
    "merchant_uid": "order_id_8237352",  
    "status": "paid"  
  }  

#### Response Structure  
