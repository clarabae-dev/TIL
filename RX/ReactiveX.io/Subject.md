> ReactiveX.io의 해당 내용을 번역 및 추가한 내용입니다.
  
## Subject  
Subject는 observable을 subscribe 할 수 있는 observer이면서 동시에 observable이어서 stream으로 동작하며 항목을 배출할 수 있다.  
단일 Subject는 단일 Observable을 subscribe 하는데, 이 때 Observable이 항목들을 배출시키도록 동작한다.  
즉, 'Cold' Observable을 'Hot' Observable로 변환하기도 한다.  
  
  
  
## Subject Type  
1. AsyncSubject  

![Alt text](http://reactivex.io/documentation/operators/images/S.AsyncSubject.png)  
  
AsyncSubject는 Observable이 종료된 후, 마지막 값만 받는다.  
Observable이 아무 값도 배출하지 않으면 AsyncSubject도 아무 값도 배출하지 않는다.  
  
![Alt text](http://reactivex.io/documentation/operators/images/S.AsyncSubject.e.png)  
  
AsyncSubject는 앞선 Observer에게 맨 마지막 값을 받아 이후 Observer에 전달한다.  
앞선 Observer가 오류로 종료하면 AsyncSubject는 아무것도 배출하지 않고 발생한 오류를 그대로 전달한다.  
  
2. BehaviorSubject  
  
![Alt text](http://reactivex.io/documentation/operators/images/S.BehaviorSubject.png)  
  
Observer가 BehaviorSubject를 구독하기 시작하면 Observer는 Observable이 가장 최근에 발행한 항목 또는 초기값이나 기본값부터 발행한다.  
  
![Alt text](http://reactivex.io/documentation/operators/images/S.BehaviorSubject.e.png)  
  
Observable이 오류로 종료되면 BehaviorSubject는 아무것도 배출하지 않고 발생한 오류를 그대로 전달한다.  
  
3. PublishSubject  
  
![Alt text](http://reactivex.io/documentation/operators/images/S.PublishSubject.png)  
  
PublishSubject는 subscribe 이후 Observable이 배출하는 항목들만 Observer에게 배출한다.  
PublishSubject는 생성 시점에 즉시 항목들을 배출하기 때문에 Observer가 PublishSubject를 subscribe 하기 전까지 배출되는 항목들은 잃어버릴 수 있다.  
때문에 Observable의 모든 항목들을 배출하려면 Create을 사용해 명시적으로 'Cold' Observable을 생성하거나 ReplaySubject를 사용해야 한다.  
  
![Alt text](http://reactivex.io/documentation/operators/images/S.PublishSubject.e.png)  
  
Observable이 오류로 종료되면 PublishSubject는 아무것도 배출하지 않고 발생한 오류를 그대로 전달한다.  
  
4. ReplaySubject  
  
![Alt text](http://reactivex.io/documentation/operators/images/S.ReplaySubject.png)  
  
ReplaySubject는 Observer가 subscribe 시점과 상관없이 Observable이 배출하는 모든 항목들을 Observer에게 전달한다.  
ReplaySubject는 몇 개의 생성자 오버로드를 제공하는데, 이를 통해 처음 배출 이후 지정한 시간이 경과할 경우 오래된 항목들을 제거할 수 있다.  
  
ReplaySubject를 Observer로 사용하는 경우, 멀티스레드 환경에서 on이나 onNext 메소드를 호출하지 않도록 주의해야 한다.  
비순차적인 호출에서 어느 항목 또는 알림을 먼저 호출해야하는지 모호해질 수 있기 때문이다.  
  
  
  
출처: http://reactivex.io/documentation/ko/subject.html  