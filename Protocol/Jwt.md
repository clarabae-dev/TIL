#### Conception
JSON Web Token.  
토큰 기반 인증 방식으로 사용자의 세션 상태를 저장하는 것이 아니라,  
필요한 정보를 토큰 body에 저장해 사용자가 가지고 있고, 그것을 증명서처럼 사용한다.  
사용자는 Access Token(JWT Token)을 헤더에 실어 서버에 보낸다.  
- Self-contained(자가 수용): JWT 자체적으로 필요한 모든 정보를 포함한다.  
헤더, 실제 전달할 데이터, 검증할 수 있는 서명 데이터를 모두 포함한다.  
- OAuth와의 관계  
JWT는 토큰의 한 종류이고, OAuth는 토큰을 발급하고 인증, 인가하는 프로토콜.  

#### Structure  
<Header>.<Payload>.<Signature>  
1. Header  
- typ: 토큰 타입 지정. JWT.  
- alg: 해시 암호화 알고리즘 지정. 이 알고리즘은 토큰을 검증할 때 사용하는 Signature 단에서 사용된다.  
>{ "typ": "JWT", "alg": "HS256" }  

2. Payload  
토큰에 담을 정보를 포함. 정보의 한 조각을 'claim' 이라 부르고, name-value 한 쌍으로 이루어진다.  
토큰에는 여러 개의 claim을 넣을 수 있는데, 크게 세 종류가 있다.  
- registered claim  
토큰 자체에 대한 정보를 저장하기 위한 claim. 모두 optional하다.  
iss : 토큰 발급자 (issuer)  
sub : 토큰 제목 (subject)  
aud : 토큰 대상자 (audience)  
exp : 토큰의 만료시간 (expiration)  
      시간은 NumericDate 형식으로 되어있어야 하며 (예: 1480849147370) 언제나 현재 시간 이후로 설정해야 한다.  
nbf : 토큰의 활성 날짜 (not before)  
      NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않는다.  
iat : 토큰이 발급된 시간 (issued at)  
      이 값을 사용하여 토큰의 age 가 얼마나 되었는지 판단.  
jti : JWT의 고유 식별자. 주로 중복 처리 방지를 위해 사용.  
- public claim  
public claim의 이름은 충돌 저항성(collision-resistant)을 가지고 있어야 한다.(URI 형식)  
> { "https://velopert.com/jwt_claims/is_admin": true }  
> collision-resistant : 같은 해시 값을 생성하는 두 개의 입력값을 찾는 것이 계산상 어려워야 한다.  

- private claim  
클라이언트-서버 간 협의하에 사용되는 claim.  
public claim과는 달리 충돌 저항성이 필수가 아니기 때문에 이름 중복을 주의해야 한다.  

> Payload  
{  
    "iss": "velopert.com",  
    "exp": "1485270000000",  
    "https://velopert.com/jwt_claims/is_admin": true,  
    "userId": "11028373727102",  
    "username": "velopert"  
}  

3. Signature  
Header의 인코딩값과, Payload의 인코딩값을 합친 후,  
주어진 비밀키로 Header에서 지정했던 해쉬 알고리즘으로 Signature를 생성한다.  
