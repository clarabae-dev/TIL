#### 특정 클래스의 메소드, property에 관한 명세서
protocol SomeProtocol {  
    func someFunc() -> Int  
    var someProperty: String { get set }  
    optional func anotherFunc()  
}
- someFunc() 메소드와 someProperty의 getter, setter을 모두 구현해야한다.
- optional 키워드는 anotherFunc()은 꼭 구현할 필요가 없다는 의미.
- optional 키워드를 명시한 메소드를 사용한다면, 다음과 같이 구현여부를 확인.  
classInstance.anotherFunc?()
optional 메소드를 구현하지 않았다면, 위 메소드는 아무 역할도 하지 않을 것이다.
  
#### struct와 class
- struct와 class 모두 protocol 사용 가능.
스위프트에서 class가 protocol을 사용하면, 상속이 아닌 protocol이라 인식하고 처리.  
class는 상속과 protocol을 모두 사용 가능.
- struct와 class는 여러 개의 프로토콜을 사용할 수 있다.
  
#### 동일성, 동등성  
1. Equatable  
값의 동일성을(==) 비교하는 프로토콜이다.  
2. Identifiable  
주민등록번호처럼 식별이 가능하게 해주는 프로토콜이다.  
Identifiable은 내부적으로 Hashable 프로토콜을 준수하는 id를 식별자로 갖는다.  