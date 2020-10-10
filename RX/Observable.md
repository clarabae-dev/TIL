## Observable  
ReactiveX에서 observer는 Observable을 subscribe 할 수 있다.  
observer는 Observable이 내뱉는 모든 아이템 또는 sequence에 대해 반응한다.  
이런 패턴은 Observable이 요소를 내뱉는 것을 기다리는 동안 차단할 필요가 없기 때문에 동시 작업을 가능하게 한다.  
대신, observer 형태의 보초를 만들어 Observable의 행동에 적절히 반응할 준비를 한다.  
  
  
  
## Establishing Observers  


출처: http://reactivex.io/documentation/observable.html