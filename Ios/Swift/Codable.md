### CodingKey  
인/디코딩 시점에 키로 사용할 수 있는 타입이다.  
서버의 스네이크 타입 <-> 카멜 케이스간 전환에 용이하다.  
  
```swift
struct ExpectedPrice: Decodable {
    let max: Int
    let min: Int
    enum CodingKeys: String, CodingKey {
        case max = "max_price"
        case min = "min_price"
    }
}
```  
  