### 특징
- 변수 선언
struct에서 let 키워드를 사용하면, 변수들은 상수처럼 사용된다.
var 키워드를 사용하면, 변수들은 '변수'로 사용할 수 있다.
- Mutating Functions
struct는 기본적으로 property의 수정을 제한하고 있다.
mutating 키워드를 사용하면, var로 선언된 struct의 내부 속성 값을 변경할 수 있다.
초기화 메소드인 init() 은 mutating 키워드 없이도 사용 가능하다.
- Memory Issues In a Multithreaded Environment
struct는 멀티스레드 환경에서 객체를 전달할 때 메모리 문제를 해결한다.
- String, Array, Dictionary, Int, Float, Boolean
스위프트의 표준 라이브러리 데이터 객체들은 대부분 struct 로, 값 객체이다.

### Commons between Struct and Class
- 변수와 함수를 정의 가능
- init() 을 활용해 생성자 또는 초기화 메소드를 정의 가능
- extension을 통해 확장 가능
- Protocol Oriented Programming, POP 구현을 위해 protocol을 사용

### Difference between Struct and Class
- class는 상속을 지원한다.
UIViewController를 상속받아 직접 뷰 컨트롤러 하위 클래스를 만들 수 있다.
- class는 deinitialization를 지원한다.
클래스가 파괴되기 전, 함수를 호출할 수 있다.
- class는 참조 타입이고, struct는 값 타입이다.

> extension
extension은 기존 class, struct, enum, protocol에 새로운 기능을 추가한다.

> deinitialization
클래스 인스턴스가 해지되기전에 즉각 호출되며, initializer의 init 키워드와 비슷하게 deinit 키워드를 사용한다.
클래스 타입에서만 사용 가능하다.
