> RxSwift github의 해당 내용을 번역한 내용입니다.
  
## Hot and Cold Observables  
Observable이 항목을 배출하는 순간은 언제일까? 배출 순간은 Observable에 따라 다르다.  

'Hot' Observable은 자신이 생성되자마자 배출하기 시작한다.  
나중에 Observable을 subscribe하는 observer는 언제든 sequence를 observe할 수 있다.  

'Cold' Observable은 observer가 subscribe 할 때까지 배출하지 않고 기다린다.  
Observable은 배출 전 모든 observer가 subscribe를 시작했는지 확인한다.  
그래서 Observable을 subscribe하는 observer는 시작부터 모든 sequence를 볼 수 있다.  
  
  
  
참조: https://github.com/ReactiveX/RxSwift/blob/main/Documentation/HotAndColdObservables.md  