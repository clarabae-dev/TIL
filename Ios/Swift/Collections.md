1. Set  
- 순서 상관없이, 중복을 허용하지 않는 collection.  
*A set stores distinct values of the same type in a collection with no defined ordering.*  
- 성능이 중요하거나 대량의 데이터 입력이 예상될 때 활용하면 좋다.  
이 때, Set을 성능에 최적화시키는 Hashable 프로토콜을 준수하는 것이 좋다.  
collection의 크기와 상관없이 요소를 조회하는데 동일한 시간이 소요된다.  
- Set은 Hashable을 구현하기 나름이다.  
  public func hash(into hasher: inout Hasher) 내부 구현에 따라 동일 객체 판단을 결정할 수 있다.  
  객체의 일부 값만 hashValue 생성에 활용하는 방식도 가능하다.  
  Ex. Set의 KeyType으로 Model을 할당하기 위해 Hashable 구현.  
  ```swift
  extension Model: Hashable {  
  	static func == (lhs: Model, rhs: Model) -> Bool {  
  		return lhs.hashValue == rhs.hashValue  
  	}  
  	public func hash(into hasher: inout Hasher) {  
  		hasher.combine(self.id)  
  	}  
  }  
  ```
- Set.insert: 동일한 값이 있으면, 값이 set에 들어가지 않는다. Set에 추가를 시도한 값이 반환되며, 만약 값이 들어가면 nil이 반환된다.  
- Set.update: 동일한 값이 있어도 값이 Set에 들어간다. 대신 기존에 있던 값이 반환되며, 동일한 값이 없었다면, nil을 반환한다.  
- Set.remove: 값을 삭제한다. 값이 삭제된다면 삭제된 값을 반환하며, 값이 없으면 nil을 반환한다.  