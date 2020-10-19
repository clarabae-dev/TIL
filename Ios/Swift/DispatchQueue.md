## Grand Central Dispatch    
Swift에서 동시성 작업을 수행하는 API이다. 주로 네트워크 작업을 수행하면서 동시에 사용자 인터렉션을 막지 않고자 할 때 사용한다.  
GCD를 활용해 동시성, 멀티스레딩 작업을 할 때에는 상황에 맞게 적절한 queue와 QoS를 선택해야 한다.  
  
  
  
## Dispatch Queues  
GCD는 멀티 스레딩 작업을 위해 thread-safe한 dispatch queue를 제공한다.  
dispatch queue는 FIFO 순으로 작업을 시작하지만, 작업 완료순은 보장하지 않는다.  
  
*Queue는 자료구조의 하나로, 먼저 입력한 데이터가 먼저 출력되는 FIFO: First In First Out 구조로 저장되는 형식이다.*  
  
dispatch queue에는 다음 세가지 종류가 있다.  
1. Main Queue (serial): main thread에서 처리되는 serial queue이다(main thread != main queue). 모든 UI 작업은 main queue에서 수행해야 한다.  
2. Global Queues (concurrent): 전체 시스템에 공유되는 concurrent queue이다. 4가지 QoS를 활용한다.  
3. Custom/Private Queues (serial 또는 concurrent): 개발자가 임의로 정의하는 queue로 global queue에서 수행된다.  
serial, concurrent 모두 정의할 수 있지만 기본적으로 serial queue를 만들고 싶을 때 주로 쓰인다.  
같은 serial queue인 main queue에서 처리하기에는 부적합하지만 백그라운드에서 serial로 동작해야하는 작업을 수행할 때 사용한다.  
  
  
### Quality of Service  
어떤 작업을 멀티스레딩으로 concurrent 하게 처리하고자 할 때 global queue를 쓰게 된다.  
그 작업의 우선순위를 지정할 때 사용하는 것이 QoS이다. QoS는 중요도와 우선순위에 따라 다음 네가지로 구분된다.  
  
1. userInteractive  
중요도가 높고 즉각적인 반응이 요구되는 작업에 가장 많은 자원을 쓰는 QoS이다.  
UI 업데이트, 이벤트 핸들링 등 가볍고 신속한 처리가 필요한 작업 용도이다. global queue 항목임에도 메인 스레드에서 실행되는 QoS이다.  
2. userInitiated  
userInteractive 만큼은 아니지만 유저가 빠른 결과를 기대할 때 사용하는 QoS이다.  
유저가 실행시킨 작업을 비동기적으로 처리한다. 유저가 블록당하지 않으면서도 빠른 결과를 기대할 때 사용한다.  
3. utility  
시간이 다소 걸리는 작업을 처리한다. 프로그래스바와 같이 유저에게 처리 중인 모습을 보여주기도 한다.  
계산, I/O, 네트워킹, 데이터 피드 등의 작업에 주로 사용한다.  
4. background  
유저가 인지하지 못하는 뒷단에서 실행한다. 유저 인터렉션도 필요없고 급히 필요하지도 않은 작업들이 수행된다.  
  
```swift
DispatchQueue.global(qos: .userInitiated).async { // Move to background thread(global queue) and start right now(async)
    let image = self.loadImage()
    DispatchQueue.main.async { // Turn back to the main queue to update the UI
        self.imageView.image = image
    }
}
```  
  
동기이던 비동기이던, serial queue이던 concurrent queue이던 관계없이 단일 작업 안의 모든 코드는 한 줄씩 수행된다.  
Concurrency, 동시성은 작업이 여러 개일 때만 해당한다.  
  
### Serial and Concurrent  
1. Serial Dispatch Queue: 각 queue는 한번에 하나의 작업만을 실행하고 그 작업이 종료되어야 새로운 작업을 실행한다.  
2. Concurrent Dispatch Queue: 각 queue는 한번에 여러 작업을 실행할 수 있고, 작업은 그들이 추가된 순서로 계속 시작된다. 종료 순서는 알 수 없다.  
  
![Alt text](https://www.swiftdevcenter.com/wp-content/uploads/2019/12/Serial-Concurrent-Queue.jpg)  
  
### Synchronous and Asynchronous  
Synchronous 방식은 작업이 종료된 후 제어권을 넘겨주므로 호출자는 이전 작업이 종료되기를 기다려야 한다.  
Asynchronous 방식은 즉시 제어권을 넘겨줘서 메인 스레드의 실행을 막지 않는다.  
  
  
  
출처:  
http://blog.naver.com/PostView.nhn?blogId=jdub7138&logNo=220949191761&parentCategoryNo=&categoryNo=136&viewDate=&isShowPopularPosts=true&from=search  
https://www.swiftdevcenter.com/grand-central-dispatch-tutorial-swift-5/  