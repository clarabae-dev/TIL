## Grand Central Dispatch  
> GCD는 멀티코어 프로세서와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술이다. -위키피디아-  
  
GCD는 개발자가 직접 스레드를 만들고 관리하지 않고도 멀티 스레드 코드를 작성할 수 있도록 추상화되어 있다.  
개발자는 GCD를 활용해 작업을 예약하고, 시스템이 리소스를 최대한 활용하여 이 작업을 수행한다.  
GCD는 필수 스레드 생성을 처리하고 해당 스레드에 대한 작업을 예약하여 시스템이 스레드 관리를 부담하게 한다.  
  
GCD의 가장 큰 장점은 concurrency한 코드를 작성할 때 하드웨어 리소스를 걱정하지 않아도 된다는 것이다.  
  
  
## Dispatch Queues  
GCD의 주된 기능으로, FIFO 구조로 작업을 시작한다. 작업 완료 시간은 FIFO가 보장하지 않는다.  

*Queue는 자료구조의 하나로, 먼저 입력한 데이터가 먼저 출력되는 FIFO: First In First Out 구조로 저장되는 형식이다.*  
  
Dispatch Queue에는 다음 세가지 종류가 있다.  
1. Main Dispatch Queue (serial, pre-defined)  
2. Global Queues (concurrent, pre-defined)  
3. Private Queues (serial 또는 concurrent 일 수 있고, 직접 생성). 
  
모든 앱은 메인 스레드에서 작업을 수행하는 serial queue인 Main Queue를 사용한다.  
Main Queue는 UI를 그리고 유저의 상호작용에 응담해야할 책임이 있다.  
네트워크 통신과 같은 오랜 시간이 소모되는 작업을 Main Queue에서 처리하면, 유저 입장에서는 앱이 동작을 멈춘 것처럼 보인다.  
  
이를 보완하기 위해 Main Queue 외에 미리 정의된 다양한 동시성 큐를 활용할 수 있다.  
1. QoS 큐에 담아 우선순위를 높여 처리하기(유저 상호작용).  
```swift
DispatchQueue.global(qos: .userInteractive).async {
    print("We're on a global concurrent queue!") 
}
```  
  
2. QoS 큐 없이 기본 우선순위대로 글로벌 큐에 담아 처리하기.  
```swift
DispatchQueue.global().async {
    print("Generic global queue")
}
```  
  
3. 직접 큐를 만들어 처리하기(Private Queues).  
```swift
let serial = DispatchQueue(label: "com.besher.serial-queue")
serial.async {
    print("Private serial queue")
}
```  
  
기본적으로 private queue는 serial한 큐이지만, attributes 속성을 추가하여 concurrent한 큐를 만들 수 있다.  
```swift
let concurrent = DispatchQueue(label: "com.besher.serial-queue", attributes: .concurrent)
```  
  
큐에 담은 작업은 sync 또는 async 함수를 사용하여 큐에서 사용할 모든 코드를 참조 할 수 있다.  
큐에서 사용하게 될 코드는 anonymous closure로 덧붙일 수 있다.  
```swift
DispatchQueue.global().async {
    print("Anonymous closure")
}
```  
  
또는 DispatchWorkItem 안에 추후에 수행할 코드를 덧붙일 수 있다.  
```swift
let item = DispatchWorkItem(qos: .utility) {
    print("Work item to be executed later")
}
```  
  
동기이던 비동기이던, serial queue이던 concurrent queue이던 관계없이 단일 작업 안의 모든 코드는 한 줄씩 수행된다.  
Concurrency, 동시성은 작업이 여러 개일 때만 해당한다.  
  
### Serial vs Concurrent  
분산처리한 작업을 serial queue는 하나의 스레드에서 처리하고, concurrent queue는 여러 개의 스레드에서 처리한다.  

serial queue는 해당 큐가 얼마나 많은 작업을 처리하는지와 관계없이, 한 번에 둘 이상의 스레드에서 작업을 처리하지 않는다.  
따라서 작업은 FIFO로 시작되고 FIFO로 종료되도록 보장된다.  
또한 sync 호출 등으로 serial queue를 차단하면 해당 queue에 대한 모든 작업은 차단이 끝날 때까지 중단된다.  
  
concurrent queue는 여러 스레드를 생성 할 수 있으며 시스템은 생성되는 스레드 수를 결정한다.  
작업은 항상 FIFO로 시작되지만, queue는 다음 작업을 시작하기 위해 이미 시작한 작업이 완료될 때까지 기다리지 않기 때문에 concurrent queue의 작업은 완료 순서를 보장하지 않는다.  
concurrent queue에서 차단 명령을 수행하면 이 queue의 다른 스레드를 차단하지는 않는다.  
  
serial과 concurrent 개념은 단일 큐의 동작 방식에 관한 내용으로, 모든 큐들은 상호간에 concurrent하다.  
즉, 두 개의 서로 다른 serial 큐들을 생성하고 그 중 하나를 차단하더라도, 다른 serial 큐는 영향을 받지 않는다.  
두 개의 큐를 순차적으로 종료시키고 싶다면, 하나의 큐는 sync한 방식으로 변경하면 된다.  
그럼 해당 큐는 현재 수행 중인 큐를 막고 실행되어 먼저 종료될 것이다.  
```swift
let serial1 = DispatchQueue(label: "com.besher.serial1")
let serial2 = DispatchQueue(label: "com.besher.serial2")

serial1.sync { // <---- we changed this to 'sync'
    for _ in 0..<5 { print("🔵") }
}
// we don't get here until first loop terminates
serial2.async {
    for _ in 0..<5 { print("🔴") }
}
```  
  
또는 serial 큐를 하나만 생성하고 두 개의 작업을 담아도 작업은 순차적으로 종료될 것이다.  
```swift
let serial = DispatchQueue(label: "com.besher.serial") // 직접 생성한 큐는 기본 serial.

serial.async {
    for _ in 0..<5 { print("🔵") }
}

serial.async {
    for _ in 0..<5 { print("🔴") }
}
```  
  
concurrent 큐이어도 sync 방식으로 수행하면 순차적으로 종료될 것이다.  
```swift
let concurrent = DispatchQueue(label: "com.besher.concurrent", attributes: .concurrent)

concurrent.sync {
    for _ in 0..<5 { print("🔵") }
}

concurrent.async {
    for _ in 0..<5 { print("🔴") }
}
```  
  
  
serial queue는 cpu 최적화와 캐싱을 활용할 때 이점이 있으며, context switching 횟수를 줄여준다.  
애플은 앱의 서브 시스템 당 하나의 serial queue로 시작할 것을 권장한다.(네트워킹에 큐 하나, 파일 압축에 큐 하나..)  
성능 문제가 발생할 때, concurrent queue가 도움이 된다면 도입할 수 있다.  
  
  
  
출처:
https://medium.com/flawless-app-stories/concurrency-visualized-part-1-sync-vs-async-c433ff7b3ebe  
https://medium.com/flawless-app-stories/concurrency-visualized-part-2-serial-vs-concurrent-fd04e32c20a9