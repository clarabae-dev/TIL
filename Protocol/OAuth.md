#### Conception  
Open Authorization, Open Authentication  
애플리케이션(Service Provider)의 유저 비밀번호를 Third party 앱에 제공하지 않고 인증, 인가할 수 있는 프로토콜  
사용자의 권한에 따라 접근할 수 있는 데이터가 다르도록 설정 가능   

#### Term  
- Resource Owner: Service Provider에 계정을 가지고 있으면서, Consumer 앱을 이용하려는 사용자  
- Service Provider: OAuth를 사용하는 Open API를 제공하는 서비스  
- Authorization Server: Service Provider의 인증 서버  
- Resource Server: Service Provider의 Rest API 서버  
- Client: OAuth 인증을 통해 Service Provider의 기능을 사용하려는 Third party 앱 또는 웹 서비스  
- Request Token: Client가 Service Provider에게 접근 권한을 인증받기 위해 사용하는 값  
  인증이 완료된 후에는 Access Token으로 교환  
- Access Token: 인증 후 Client가 Service Provider의 자원에 접근하기 위한 키를 포함한 값  
- Token Secret: 주어진 토큰의 소유권을 인증하기 위해 Resource Owner가 사용하는 Secret  

#### Various Authentication Methods
1. Authorization Code Grant  
- Client가 Redirect URL을 포함하여 Authorization server 인증 요청을 한다.  
- Authorization Server는 유저에게 로그인창을 제공하여 유저 인증 절차를 거친다.  
- Authorization Server는 Authorization code를 Client에게 제공한다.  
- Client는 Authorization code를 포함하여 Authorization Server에 Access Token을 요청한다.  
- Authorization Server는 Client에게 Access token을 발급한다.  
- 발급받은 Access Token을 이용하여 Resource Server의 자원에 접근할 수 있게 된다.  
- 토큰이 만료된다면 Refresh Token을 이용하여 토큰을 재발급 받을 수 있다.  

2. Implicit Grant  
- Client는 Authorization Server에 인증을 요청한다.  
- Resource Owner는 Authorization Server를 통해 인증한다.  
- Authorization Server는 Access Token을 포함하여 Client의 Redirect url을 호출한다.  
- Client는 해당 Access Token이 유효한지 Authorization Server에 인증 요청한다.  
- Authorization Server는 그 토큰이 유효하다면 토큰의 만기시간을 함께 리턴한다.  
- Client는 Resource Server에 접근할 수 있게 된다.  

Resource Owner Password Credentials Grant
Client Credentials Grant
Device Code Grant
Refresh Token Gran
