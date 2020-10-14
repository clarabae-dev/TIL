## Protocol-Oriented Programming  
  
  
### 프로토콜 지향 언어  
Swift 표준 라이브러리에서 타입 구현부를 보면 대부분 클래스가 아닌 구조체로 구현되어 있다.  
상속이 불가능한 구조체로 다양한 공통 기능을 가질 수 있는 이유는 protocol과 extension을 활용했기 때문이다.  
protocol로 메소드, 프로퍼티 등 청사진을 그리고, extension으로 미리 프로토콜 요구사항을 초기 구현하여 중복 코드를 피한다.  
  
```swift
protocol Talkable {
    var topic: String { get set }
    func talk(to: Self)
}

extension Talkable {
    func talk(to: Self) {
        print("\(to)! \(topic)")
    }
}
```  
  
프로토콜을 준수하는 타입이 초기 구현과 다르게 구현해야 한다면, 재정의하면 된다.  
  
### Why use POP?  
1. 상속은 참조 타입인 클래스에서만 가능하다.  
참조 타입이 아닌 타입을 활용하여 참조 추적을 하지 않고, 상속을 하지 않고도 기능을 구현할 수 있다.  
2. 기능의 모듈화  
프로토콜 단위로 기능을 묶어 표현하고 초기 구현을 해둘 수 있고, 다중 상속이 가능하다.  
  
  
  
출처: https://blog.yagom.net/531/  