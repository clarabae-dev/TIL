## Struct  
  
  
### 특징  
1. 변수 선언  
struct에서 let 키워드를 사용하면, property를 상수처럼 사용한다.  
var 키워드를 사용하면, property를 '변수'로 사용할 수 있다.  
2. Mutating Functions  
struct는 기본적으로 property의 수정을 제한하고 있다.  
mutating 키워드를 사용하면, var로 선언된 struct의 내부 property 값을 변경할 수 있다.  
초기화 메소드인 init() 은 mutating 키워드 없이도 사용 가능하다.  
3. String, Array, Dictionary, Int, Float, Boolean  
스위프트의 표준 라이브러리 데이터 객체들은 대부분 struct 로, 값 객체이다.  
  
  
  
## Struct and Class  
  
  
### Commons  
1. 변수와 함수를 정의할 수 있다.  
2. init() 을 활용해 생성자 또는 초기화 메소드를 정의할 수 있다.  
3. extension을 통해 확장할 수 있다.  
4. Protocol Oriented Programming, POP 구현을 위해 protocol을 사용할 수 있다.  
  
### Difference  
1. class는 참조 타입이다.  
- 힙 메모리 영역에 저장되며 ARC로 객체의 메모리를 관리한다.  
- 참조가 복제되기 때문에 공유할 수 있다.  
- 상속을 지원한다.  
- deinitialization를 지원한다.  
클래스가 deinit 되기 전, 함수를 호출할 수 있다.  
2. struct는 값 타입이다.  
- 값 자체가 복제되기 때문에 공유할 수 없다.  
- 상속을 지원하지 않는다.  
- let 키워드를 사용하면 property를 상수로 사용할 수 있기에 불변성 구현에 유리하다.  
- 불변적인 인스턴스가 thread-safe하기 때문에 멀티스레딩 환경에서 안정적이다.  

> extension  
기존 class, struct, enum, protocol에 새로운 기능을 추가한다.  

> deinitialization  
클래스 인스턴스가 해지되기전에 즉각 호출되며, initializer의 init 키워드와 비슷하게 deinit 키워드를 사용한다.  
클래스 타입에서만 사용 가능하다.  