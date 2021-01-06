## Method Dispatch  
프로그램이 메소드를 호출할 때 실행할 명령어를 선택하는 방법으로 메소드가 호출될 때마다 발생한다.  
컴파일 언어의 메소드 실행 방법은 크게 3가지가 있다: **direct dispatch, table dispatch, message dispatch**  
대부분의 언어가 이 중 한두가지 방법을 지원한다. Java는 기본적으로 table dispatch를 지원하는데, final 키워드를 사용해 direct dispatch를 사용할 수도 있다.  
C++은 direct dispatch를 기본 지원하며, virtual 키워드를 사용해 table dispatch를 사용할 수 있다.  
Objective-C는 항상 message dispatch를 지원하는데, C처럼 direct dispatch의 성능을 사용할 수 있다.  
Swift는 3가지 방법을 모두 지원한다.  
  
  
  
  
## Type of Dispatch  
dispatch를 하는 이유는 프로그램이 특정 메소드 호출을 위한 실행 코드의 메모리 위치를 CPU에게 알려주기 위해서이다.  
  
  
  
### Direct Dispatch  
Static Dispatch 혹은 Compile-time Dispatch 라고도 부르며, method dispatch 방법들 중 가장 빠른 방법이다.  
컴파일러를 빌드하는 동안 호출할 항목과 시기를 이미 알고 있다.  

direct dispatch는 속도는 매우 빠른 반면, 프로그래밍 관점에서 가장 제한적인 방법이다.  
subclassing과 함께 사용하기 어려우며, extension method가 항상 direct dispatch 방식을 사용한다.  
  
  
### Table Dispatch  
Runtime Dispatch 혹은 Dynamic Dispatch 라고도 부르며, 컴파일 언어에서 동적인 행위를 구현하는 가장 일반적인 방법이다.  
각 메소드별로 함수 포인터들의 배열을 사용한다.
  
  
  
참고:  
https://www.rightpoint.com/rplabs/switch-method-dispatch-table  
https://medium.com/@venki0119/method-dispatch-in-swift-effects-of-it-on-performance-b5f120e497d3  