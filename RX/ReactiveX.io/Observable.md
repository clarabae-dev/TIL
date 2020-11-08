> ReactiveX.io의 해당 내용을 번역 및 추가한 내용입니다.
  
## Observable  
Observable은 대상을 관찰할 수 있는 형태로 바꾸어준다.  
ReactiveX에서 observer는 Observable을 subscribe 할 수 있다.  
observer는 Observable이 내뱉는 모든 아이템 또는 sequence에 대해 반응한다.  
이런 패턴은 Observable이 요소를 내뱉는 것을 기다리는 동안 차단할 필요가 없기 때문에 동시 작업을 가능하게 한다.  
대신, observer 형태의 보초를 만들어 Observable의 행동에 적절히 반응할 준비를 한다.  
  
  
  
## Establishing Observers  
비동기 모델의 흐름은 다음과 같다.  
1. 비동기 호출의 반환 값으로 작업을 수행하는 메소드를 정의한다.  
2. 비동기 호출을 Observable이라 정의한다.  
3. observer를 subscribe하여 해당 Observable에 연결한다. 이 때 Observable의 작업도 시작한다.  
4. 비동기 호출 즉, Observable이 값을 반환될 때마다 observer의 메소드는 그 값을 활용하여 작업을 수행한다.  
  
  
### onNext, onCompleted, and onError  
Subscribe 방법은 observer를 Observable에 연결하는 방법이다. observer는 다음 메소드들을 구현할 수 있다.  
1. onNext  
Observable이 아이템을 내보낼 때마다 호출하는 메소드이다. 이 메소드는 Observable이 내보내는 아이템을 파라미터로 사용한다.  
2. onError  
Observable이 다음 아이템을 내보내는 것을 실패하거나 오류가 발생하였을 때 호출하는 메소드이다.  
onError 메소드가 호출되면, 더이상 onNext 또는 onCompleted 메소드가 호출되지 않는다.  
onError 메소드는 오류의 원인을 파라미터로 사용한다.  
3. onCompleted  
Observable이 아무 오류없이 마지막 onNext 메소드가 호출되면, 호출하는 메소드이다.  
  
onNext는 보통 아이템을 내보낼 때 호출되는 반면, onCompleted와 onError는 알려야 하는 때에 호출된다.  
  
### Unsubscribing  
unsubscribe 메소드는 Subscriber가 현재 subscribe 하고있는 Observable들 중 그 어떤 것도 더이상 subscribe하지 않고자 할 때 호출할 수 있다.  
observer가 하나도 없는 Observable들은 아이템을 내보내는 것을 중단할 수 있다.  
  
subscribe를 중단함으로써 발생하는 결과들은 Observable에 적용된 연산자들에 전달되고, 각 연산자들은 아이템 배출을 중단하게 된다.  
그러나 즉각적인 중단이 보장되지는 않고, observer가 없음에도 Observable이 잠시간 아이템을 배출할 수도 있다.  
  
  
  
## Hot and Cold Observables  
Observable이 아이템을 배출하기 시작하는 순간은 Observable 자신에게 달려있다.  
hot observable은 observable이 생성되자마자 아이템을 배출하기 시작한다.  
때문에 나중에 subscribe하기 시작한 observer는 중간부터 sequence를 관찰할 수 있다.  
cold observable은 아이템을 배출하지 않고 observer가 자신을 subscribe할 때까지 기다린다.  
때문에 observer는 sequence 관찰을 처음부터 시작할 수 있음을 보장받는다.  
  
ReactiveX에는 Connectable Observable도 있는데, observer의 subscription과 관계없이 Connect 메소드가 호출되기 전까지는 아이템을 배출하지 않는다.  
  
  
  
## Composition via Observable Operators  
Observable과 observer는 ReactiveX의 시작에 불과하며, observer 패턴을 조금 확장한 것일 뿐이라 콜백보다는 이벤트 시퀀스를 처리하는 것에 더 적합하다.  
ReactiveX의 진정한 힘은 Observable이 배출하는 아이템을 변형하고 결합하고 조작하고 작업할 수 있는 연산자에 있다.  
ReactiveX 연산자는 비동기적 시퀀스들을 선언적 방식으로 구성할 수 있다.  
  
  
### Chaining Operators  
대부분의 연산자들이 Observable을 연산하고 Observable을 반환하기 때문에 연산자들을 연쇄적으로 적용할 수 있다.  
각 연산자는 이전 연산자가 수행한 결과인 Observable을 수정한다.  
  
  
  
출처: http://reactivex.io/documentation/observable.html  