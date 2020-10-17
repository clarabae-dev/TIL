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
  
### 비동기적인 데이터 스트림의 집합체  
반응형 프로그래밍에서는 기본적으로 모든 요소를 스트림으로 취급한다.  
즉, 모든 데이터의 흐름을 시간순서에 의해 전달되어지는 스트림으로 본다.  
각각의 스트림은 새로 만들어(branch)져서 새로운 스트림이 될 수도 있고, 여러개의 스트림이 합쳐(merge)질 수 도 있다.  
스트림은 map, filter과 같은 함수형 메소드를 이용하여, immutable하게 처리할 수 있다.  
스트림을 listening함으로써 데이터의 결과값을 얻는다. 이를 subscribe라고 표현한다.  
  
### ReactiveX  
ReactiveX란, observable stream을 활용해 비동기 프로그래밍을 하기 위한 API다.(*stream: 연속되는 요소*)  
  
  
  
출처: http://reactivex.io/intro.html