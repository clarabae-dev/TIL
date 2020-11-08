## Reactive Programming  
1. 개발자에게 Reactive Programming 이란  
비동기적인(Async) 데이터 스트림의 집합체  
Observer 패턴을 활용해 발생하는 비동기 이벤트를 처리  
2. 사용자에게 Reactive Programming 이란  
실시간으로 반응하는 환경  
3. Imperative Programming과 대비되는 개념  
a = b + c  
명령형 프로그래밍에서는 재연산 명령이 들어오지않는 한 한번 계산된 값은 바뀌지 않는다.  
반응형 프로그래밍에서는 b와 c의 값이 변경될 때마다 바로 재연산이 수행되어 a 값이 변경된다.  
ex. DataBinding  
  
Reactive Programming은  
1. 데이터 흐름을 먼저 정의하고,  
2. 데이터가 변경되었을 때,  
3. 연관되는 함수나 수식이 업데이트 된다.  
  
Swift에는 Callback, Delegate, Notification 등 비동기를 지원하는 다양한 API들이 존재한다.  
위 API들은 데이터를 받아온 후, 개발자가 명시적으로 UI 업데이트를 해주어야 하는 반면, Reactive Programming을 활용하면, UI 업데이트 로직을 자동화해준다.  
데이터를 구독(subscribe)하여 그 변경을 관찰(observe)하고 있기 때문에 자동화가 가능하다.

### 비동기적인 데이터 스트림의 집합체  
반응형 프로그래밍에서는 기본적으로 모든 요소를 스트림으로 취급한다.  
즉, 모든 데이터의 흐름을 시간순서에 의해 전달되어지는 스트림으로 본다.  
각각의 스트림은 새로 만들어(branch)져서 새로운 스트림이 될 수도 있고, 여러개의 스트림이 합쳐(merge)질 수 도 있다.  
스트림은 map, filter과 같은 함수형 메소드를 이용하여, immutable하게 처리할 수 있다.  
스트림을 listening함으로써 데이터의 결과값을 얻는다. 이 행위를 subscribe라고 표현한다.  
  
### ReactiveX  
ReactiveX란, observable stream을 활용해 비동기 프로그래밍을 하기 위한 API다.(*stream: 연속되는 요소*)  
Reactive Programming을 가능하게 해주는 구현체이다.  
  
  
  
참조:  
http://reactivex.io/intro.html  
https://zeddios.tistory.com/689  