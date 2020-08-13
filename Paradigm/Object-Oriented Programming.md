#### Dependency Inversion Principle, 의존성 역전 원칙  
A class가 B class를 참조한다.  
class A {  
  B b = new B();  
}  
이 경우, A class는 B class를 의존하고 있다. A -> B  
  
B class를 추상화한 C interface를 만든다.  
A class는 C interface를 통해 B class에서 필요한 메소드를 참조할 수 있다.  
class A {  
  C c = new B();  
}  
이 경우, A class는 C interface를 의존하고, 의존도가 없던 B class도 C interface를 의존한다. A -> C <- B  
위와 같은 상황을 '의존성이 역전된다'고 표현한다.  