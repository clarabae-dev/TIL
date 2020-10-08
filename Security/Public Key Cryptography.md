현대 암호 알고리즘은 대칭형, 비대칭형 두가지로 구분된다.  
1. 대칭형 암호 알고리즘: 암호화 키와 복호화 키가 동일한 알고리즘  
2. 비대칭형 암호 알고리즘: 암호화 키와 복호화 키가 서로 다른 알고리즘  
  
  
  
## 대칭형 암호 알고리즘  
• 암복호화 속도가 비대칭형 암호 알고리즘보다 빠르다.  
• 암호화할 때 데이터 증가가 없다. 크기가 증가하지 않는다는 것은 암호화된 데이터의 크기가 평문과 같다는 것으로 네트워크 대역폭을 추가적으로 필요로 하지 않는다.  
• 키가 임의로 지정된다. 길이는 보안 수준에 따라 128비트 또는 256 비트로 설정된다.  
  
  
### Key Bootstrapping, Key Agreement Problem  
대칭형 암호 알고리즘은 송신자와 수신자가 동일한 키를 가져야하기 때문에 전달 및 관리에 어려움이 생긴다.  
대칭형 암호 알고리즘을 보완하기 위한 방법은 다음 두가지가 있다.  
1. 비대칭형 암호화 알고리즘  
2. 실제 키를 전송하지 않고 송수신자가 동일한 키를 생성할 수 있도록 하는 알고리즘을 사용. 대표적으로 Diffie-Hellman 알고리즘이 있다.  
  
  
  
## 비대칭형 암호 알고리즘  
• 타인에게 절대 노출되어서는 안되는 개인키와 개인키를 토대로 만든 공개키 한 쌍의 형태이다.  
• 한쪽 키가 공개되어야 사용이 가능하기 때문에 공개키 알고리즘이라고도 부른다.  
• 공개키와 개인키 사이에 반드시 수학적 관계, 패턴이 있어야한다.  
• 공격자가 패턴을 탈취할 수 있으며, 대칭 알고리즘과 동등한 수준의 보안을 제공하기 위해 비대칭키는 훨씬 길어야 한다. 128비트 대칭키와 2048 비트 비대칭키의 보안이 비슷하다.  
• 비대칭형 암호는 암복호화가 대칭형 암호화에 비해 현저히 느리다.  
현실적으로 비대칭형 암호를 이용해 대칭형 암호 키를 배송하고 실제 암호문은 대칭형 암호를 사용하는 등의 상호보완적인 이용이 일반적이다.  
• 비대칭 암호화와 디지털 서명 두가지 방식이 있다.  
1. 비대칭 암호화 : 공개키로 암호화한 내용은 공개키에 대응하는 비밀 키를 가지고 있는 사용자만 열어볼 수 있다. 데이터 보안에 중점을 둔다.  
2. 디지털 서명 : 특정한 비밀 키로 만들었다는 것을 누구나 확인할 수 있다. 인증과정에 중점을 둔다.  
  
  
### 데이터 전송 방식  
1. A는 공개키와 개인키를 생성한다.  
A의 공개키로 암호화된 데이터는 A의 개인키로만 복호화가 가능하다.  
A의 개인키로 암호화된 데이터는 A의 공개키로만 복호화가 가능하다.  
2. B도 공개키와 개인키를 생성한다.  
3. A와 B는 서로에게 각자의 공개키를 알려준다.  
4. A는 B에게 데이터를 전송할 때 B의 공개키로 데이터를 암호화하여 전송한다.  
5. 암호화된 데이터는 그에 대응하는 개인키를 가지고 있는 B만 복호화할 수 있다.  

### 디지털 서명  
디지털 서명은 인증서 형태로 발급되는 자신만의 디지털 인감 도장이며 안전한 서명이다.  
인터넷 환경에서 특정 사용자를 인증하기 위한 목적으로 사용된다.  
비대칭 암호화와 달리 암호화를 사용할 수도 있고 하지 않을 수도 있다.  
일례로 비트코인에서 사용하는 디지털 서명 알고리즘, ECDSA는 공개-개인키 쌍을 활용하지만 암호화를 전혀 사용하지 않는다.  
  
디지털 서명은 자신을 다수에게 증명하는 기능이므로 자신만 아는 개인키로 암호화한다.  
개인키로 암호화한 디지털 서명은 다수의 타인이 볼 수 있으므로 공개키를 사용해 복호화되어 원문과 비교될 수 있다.  
  
복호화 과정은 다음과 같다.  
1. 받은 문서를 RSA 알고리즘의 비공개키로 복호화하여 디지털 서명문을 얻는다.  
2. 디지털 서명문을 송신자 인증에 필요한 디지털 서명 공개키로 복호화해 원문을 얻는다.  

디지털 서명 과정에서 RSA 알고리즘을 사용하는 이유는 전송 과정에서 보안 문제를 해결하기 위해서이다.  
  
### 종류  
1. RSA  
• 비대칭 암호화 알고리즘에서 가장 많은 지지를 받으며 오늘날 산업 표준으로서 사용되는 방법.  
• 기본적인 정수론, 즉 소수를 이용. 중요 정보를 두개의 소수로 표현한 후, 두 소수의 곱을 힌트와 함께 암호로 사용한다.  

2. Diffie-Hellman, 디피-헬만  
• 1976년 비대칭 암호 방식을 최초로 제안한 Whitfield Diffie와 Martin Hellman이 발명한 암호화 알고리즘.  
• 두 사용자 간 공통의 암호화키를 공개하는 방식을 이용해 사전에 어떠한 교환없이도 통신망에서 안전하게 공유할 수 있는 방법을 제시한 최초의 비밀 교환 프로토콜.  
• 가장 오래된 비대칭 암호화 시스템으로 중간자 공격에 취약한 단점이 있다.  

3. 타원곡선암호, ECC, Elliptic Curve Cryptosystem  
• 타원곡선이라고도 불리는 수식으로 정의하는 특수 계산법을 기반으로 암복호화를 수행하는 방식.  
• RSA/DSA와 같은 공개키 암호보다 짧은 키 길이와 빠른 연산 속도를 가지면서 동일한 수준의 보안 강도를 제공하는 암호 알고리즘.  
• 짧은 키 길이에 높은 안전성이 보장되고, 또 서명할 때의 계산을 빠르게 할 수 있다.  
  
  
  
출처:  
http://wiki.hash.kr/index.php/%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4  
https://sungjk.github.io/2016/09/30/Security.html  