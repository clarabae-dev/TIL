## iOS Architecture  
좋은 아키텍쳐의 특징은 다음과 같다.  
1. 각 객체의 역할/책임이 분명하다. 한 객체는 하나의 역할만 수행하도록 해서 복잡도를 낮춰야 한다.  
2. 테스트가 용이하다. 사전에 테스트를 통해 이슈를 보완할 수 있다.  
3. 유지보수가 용이하다. 길이가 짧고 설명이 필요하지 않은 코드를 작성해야 한다.  
  
  
### Traditional MVC  
전통적인 MVC 패턴은 Model, View, Controller로 구조를 분리한다.  

![Alt text](https://miro.medium.com/max/1000/1*E9A5fOrSr0yVmc7Kly5C6A.png)  
  
전통적인 MVC 패턴은 Model, View, Controller가 밀접하게 연관되어 있어 결합도가 높다.  
  
### Apple's MVC  
전통적인 MVC 패턴의 단점을 보완하기 위해 Apple이 Cocoa MVC 패턴을 제시한다.  
Cocoa MVC 패턴에서는 Controller가 Model과 View 사이를 연결해주어 Model과 View 간의 결합도를 없애준다.  
  
![Alt text](https://miro.medium.com/max/1000/1*c0aGaDNX41qu6e8E4OEgwQ.png)  
  
그러나 View와 Controller가 강하게 결합되어 있어 ViewController가 UI는 물론 View의 LifeCycle도 관리한다.  
  
![Alt text](https://miro.medium.com/max/1400/1*PkWjDU0jqGJOB972cMsrnA.png)  
  
  
  
  
출처:  
https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52  
https://jiyeonlab.tistory.com/38  