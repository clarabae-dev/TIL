출처:  
https://www.youtube.com/watch?v=c33ojJ7kE7M  
https://developer.apple.com/documentation/foundation/nscache  
https://en.wikipedia.org/wiki/Cache_replacement_policies  
  
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
- Reactive Cache로 리소스가 충분할 때는 주어진 모든 데이터를 캐싱.  
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
  
## Cache Replacement Policy  
  
### Overview  
- 캐시 메모리에 여유 공간이 없을 때 어떤 데이터를 가장 먼저 폐기할지 선택하는 알고리즘.  
- 평균 메모리 참조 시간은 다음과 같다.  

![Alt text](https://wikimedia.org/api/rest_v1/media/math/render/svg/a5b900da5f0c0e84a91d5d34965c18fc3b58b9cc)  
  
m = miss ratio = 1 - (hit ratio)  
T{m} = miss가 발생했을 때, 다음 레벨의 캐시 메모리 또는 메인 메모리에 접근하는데 소요되는 시간  
T{h}= the latency: 캐시에 데이터를 요청 후 돌려받기까지(hit) 소요되는 시간  
E = 부가적인 효과들  
  
hit ratio는 캐사에서 특정 데이터를 얼마나 자주 찾는가를 나타낸다.  
- 가장 효율적인 교체 알고리즘은 hit rate를 향상시키기 위해 더 자주 찾는 데이터를 추적한다.  
- 더 빠른 교체 알고리즘일수록 데이터를 업데이트하는데 필요한 시간을 줄이기 위해 덜 쓰는 데이터를 추적한다.  
- 교체 알고리즘은 적중률과 지연 시간 사이의 절충안을 찾는 과정이다.  
- 데이터 획득 비용: 획득비용이 더 비싼 데이터를(획득하는데 시간이 더 오래 걸림) 캐시에 유지한다.  
- 데이터 크기: 데이터 크기가 서로 다르면, 캐시는 더 작은 여러 데이터들을 저장하기 위해 더 큰 데이터를 버릴 것이다.  
- 만료될 데이터: DNS 캐시, 웹 브라우저 캐시 등은 만료된 데이터를 가지고 있다.  
  
### Policies  
1. First in first out, FIFO  
캐시는 fifo queue와 같이 동작.  
캐시는 블록 접근 여부, 빈도수 등과 관계없이 블록을 추가한 순서대로 블록을 제거한다.  
2. Last in first out, LIFO or First in last out, FILO  
캐시는 스택과 같은 방식으로 동작하고, fifo queue와는 정반대 방식으로 동작한다.  
캐시는 블록 접근 여부, 빈도수 등과 관계없이 관계없이 가장 최근에 추가된 블록을 제거한다.  
3. Least recently used, LRU  
가장 오랫동안 사용되지 않은 데이터를 제거한다.  
이 알고리즘은 데이터 사용 내역을 추적해야 하고, 항상 가장 오랫동안 사용되지 않은 데이터를 삭제하도록 하기 위해 비용이 많이 든다.  
프로세스가 주기억장치에 접근할 때마다 페이지 참조 시간을 기록해야 해서 큰 오버헤드가 발생한다.  
  
![Alt text](https://en.m.wikipedia.org/wiki/File:Lruexample.png)  
  
4. Most recently used, MRU  
LRU와 반대로, 가장 최근에 사용된 데이터를 가장 먼저 제거한다.  
MRU는 더 오래된 데이터에 접근할 확률이 높을수록 효과적이다.  
  
![Alt text](https://en.m.wikipedia.org/wiki/File:Mruexample.png)  
  
5. Pseudo-LRU, PLRU
  
![Alt text](https://en.m.wikipedia.org/wiki/File:Plruexample.png)    
  
LRU의 성능 향상 버전. 교체할 때 모든 데이터의 정확한 age를 사용하기 보다 대략적인 age 측정값을 활용하는 것이다.  
위는 트리방식의 PLRU이다. miss가 발생하면 메모리에 필요한 데이터를 적재한다.  
데이터를 적재할 곳을 선택하는 기준은 이진트리의 리프노드 포인터가 가리키는 곳이다.  
데이터를 적재한 후 적재된 곳을 가리키는 포인터들은 가리키는 방향이 반대 방향으로 바뀐다.  

6. Random replacement, RR  
데이터를 랜덤하게 폐기한다. 이 알고리즘은 데이터 접근 내역을 추적할 필요가 없다. ARM 프로세서에서 사용된다.  
7. Least-frequently used, LFU  
얼마나 자주 데이터가 필요한지 카운트한다. 가장 적게 사용된 데이터를 가장 먼저 제거한다.  
LRU 알고리즘과 비슷한데, 얼마나 최근에 블록에 접근했는지를 저장하는 대신, 블록에 접근한 횟수를 저장한다.  

> Page Fault: 페이지 부재 또는 페이지 폴트. 메모리에 적재된 페이지 중 사용하려는 페이지가 없을 때를 가리킨다.  