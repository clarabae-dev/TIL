### 특정 클래스의 메소드, property에 관한 명세서  
```swift
protocol SomeProtocol {  
    func someFunc() -> Int  
    var someProperty: String { get set }  
    optional func anotherFunc()  
}
```  

1. someFunc() 메소드와 someProperty의 getter, setter을 모두 구현해야한다.  
2. optional 키워드는 anotherFunc()은 꼭 구현할 필요가 없다는 뜻이다.  
3. optional 키워드를 명시한 메소드를 사용한다면, 다음과 같이 구현여부를 확인할 수 있다.  

```swift
classInstance.anotherFunc?()
```  
  
optional 메소드를 구현하지 않았다면, 위 메소드는 아무 역할도 하지 않을 것이다.  
  
### struct와 class  
1. struct와 class 모두 protocol을 사용할 수 있으며, 여러개의 프로토콜도 가능하다.  
2. class가 protocol을 사용하면, 상속이 아닌 protocol이라 인식하고 처리한다.  
3. class는 상속과 protocol을 모두 사용할 수 있다.  
  
### 동일성, 동등성  
1. Equatable  
값의 동일성을(==) 비교하는 프로토콜이다.  
2. Identifiable  
주민등록번호처럼 식별이 가능하게 해주는 프로토콜이다.  
Identifiable은 내부적으로 Hashable 프로토콜을 준수하는 id를 식별자로 갖는다.  
  
### Hashable  
1. 정수 hash 값을 제공하는 protocol 타입.  
Set 또는 Dictionary의 KeyType으로 Hashable을 준수하는 모든 타입을 사용할 수 있다.  
Hashable을 준수한다, 해쉬가능하다 라는 말은 그 자체로 유일하게 표현이 가능하다는 뜻이다.  
스위프트의 기본 타입(String, Int, Double.. 등)과 enum은 hashable하므로 KeyType으로 사용가능하다.  
2. hash 함수는 input/output이 한 쌍을 이룬다. 동일한 input -> 동일한 output.  
또한, 중복되는 레코드를 찾을 수 있기 때문에 매우 빠른 검색이 가능하다.  
Set이나 Dictionary는 순서를 보장하지 않되 Hashable한 KeyType을 가지므로, 검색이 빠르고, 중복을 허용하지 않는다.  
3. hashValue로 제공되는 hash 값은 임의의 두 인스턴스에 대해 동일한 정수값이다.  
같은 타입의 인스턴스 a와 b가 있을 때, a == b 이면 a.hashValue == b.hashValue이다.  
그러나 a.hashValue == b.hashValue 라고 해서 항상 a == b 가 성립하지는 않는다.  