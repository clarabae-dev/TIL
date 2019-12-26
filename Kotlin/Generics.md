#### Why Java needs Wildcard Types?  
1. Java의 generic type은 불변성을 가진다.  
List<String>은 List<Object>의 subtype이 아니다.  
2. <? extends E>  
wildcard type argument로 ?에 들어오는 타입은 E의 객체들의 collection 또는 E의 subtype 뿐이다.  
즉, 위 타입의 collection에서 E 타입의 객체들을 안전하게 읽어올 수는 있지만,  
반대로, 어떤 객체가 E subtype에 적합한지 알 수 없기 때문에 collection에 더할 수는 없다.  
wildcard type으로 유일하게 보장받을 수 있는 점은 type safety 이다.  

#### Star-projections  
타입을 알 수 없지만, 안전하게 사용하고 싶을 때, generic type의 projection을 정의할 수 있다.  
generic type의 모든 인스턴스들이 정의한 projection의 하위 타입이 될 것이다.  
코틀린에서는 star-projection 이라는 syntax를 제공한다.  
