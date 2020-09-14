출처:  
https://www.youtube.com/watch?v=c33ojJ7kE7M  
https://developer.apple.com/documentation/foundation/nscache  
  
### 메모리 계층 구조  
컴퓨터에서 데이터를 저장하는 공간의 속도와 용량은 반비례하다.  
속도가 빠른 메모리일수록 용량이 작으며, 용량이 큰 메모리일수록 속도가 느리다.  
속도와 용량 모두를 잡기에는 비용이 너무 많이 들기 때문에 특성에 맞게 역할을 나누어 사용한다.  
  
![Alt text](https://webdocs.cs.ualberta.ca/~amaral/courses/429/webslides/Topic4-MemoryHierarchy/img003.gif)  
  
### 데이터 지역성의 원리  
자주 쓰이는 데이터는 시간적 혹은 공간적으로 한 곳에 몰려있을 가능성이 높다.  
- 시간 지역성(Temporal Locality)  
ex. 반복문에서 조건변수를 선언했을 때, 해당 변수는 반복문이 끝나기 전까지 계속 쓰일 확률이 높다.  
- 공간 지역성(Spatial Locality)  
ex. 반복문에서 특정 배열에 접근했을 때, 해당 배열이 위치한 메모리 공간의 내용은 반복문이 끝나기 전까지 계속 쓰일 확률이 높다.  
  
### Cache  
추후 필요할 수도 있는 무언가를 저장하였다가 신속하게 회수할 수 있는 보관 장소로, 어떤 식으로든 보호되거나 숨겨진다.  
1. 원본 데이터와 별개로 자주 쓰이는 데이터(hot data)들을 복사해둘 캐시 공간을 마련한다.  
캐시 공간은 낮은 시간 복잡도(ex. 상수 시간 O(1))로 접근 가능한 곳을 주로 사용한다.  
2. 데이터를 달라는 요청이 들어오면, 원본 데이터에 접근하기 전, 캐시 공간부터 찾는다.  
3. 캐시에 원하는 데이터가 없거나(cache miss) 오래되어 최신성을 잃었다면(expiration) 원본 데이터에 접근한다.  
이 때, 캐시에도 해당 데이터를 복사하거나 혹은 갱신한다.  
4. 캐시에 원하는 데이터가 있으면, 캐시에서 바로 해당 데이터를 제공한다.(cache hit)  
5. 캐시 공간은 작기 때문에 공간이 모자라면 쓰지 않는 데이터부터 삭제하여 공간을 확보한다.(eviction)  
  
### NSCache Class  
- 리소스가 부족할 때 제거될 수 있는 임시 key-value 쌍을 일시적으로 저장할 때 사용하는 가변적인 컬렉션.  
- 리소스가 충분할 때는 주어진 모든 데이터를 캐싱.  
- 캐시가 시스템 메모리를 너무 많이 사용하지 않도록 다양한 자동 제거 정책을 통합.  
다른 애플리케이션에 메모리가 필요한 경우 캐시에서 일부 항목을 제거하여 메모리 사용 공간을 최소화.  
- 캐시에 락을 걸지않고도 서로 다른 스레드에서 캐시에 접근해 아이템을 추가, 제거, 쿼리할 수 있다.  
- NSCache 객체는 일시적이지만 생성 비용이 많이 드는 데이터를 임시로 저장할 때 사용한다.  
이 객체들을 재사용하면 재연산 할 필요 없기 때문에 성능상 이점이 생긴다.  
그러나 이 객체들은 앱에 중요하지 않아서 메모리가 부족하면 폐기될 수 있다.  
메모리에서 폐기되면, 그 값들은 필요해질 때 다시 재연산된다.  

> Object-C 클래스를 사용할 때, 지켜야 할 주의사항:  
> - 클래스 인스턴스만 저장  
> - NSObject 기반 키와 호환  

```swift
let cache = NSCache<NSString, MyClass>() // NSObject의 서브 클래스들인 키들과만 호환이 가능하다.
let myObject: MyClass

if let cachedVersion = cache.object(forKey: "CachedObject") {
    myObject = cachedVersion // use the cached version
} else {
    myObject = MyClass() // create it from scratch then store in the cache
    cache.setObject(myObject, forKey: "CachedObject")
}
```