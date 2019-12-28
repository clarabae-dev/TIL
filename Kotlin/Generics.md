Generics란, 클래스나 함수를 정의할 때 타입을 확실히 정하지 않는 것을 의미한다.  

#### Java Wildcard Type Argument  
- T : read/write  
- ? extends T : read only subtype wildcard  
보통 List에서 많이 활용한다.  
add(item)은 오류가 발생하지만, add(null)은 오류가 발생하지 않는다.  
- ? super T : write only supertype wildcard  

> subtype: A 타입이 필요한 모든 곳에 B 타입을 대입해도 별 문제가 없다면 B는 A의 subtype이다.  
> subclass vs subtype: A?와 A는 동일한 클래스이다. A는 A?의 subtype이고, 그 역은 성립하지 않는다.  

#### Invariance/Covariance  
generic type을 각각 다른 type argument로 인스턴스화할 경우,  
인스턴스 타입 간의 subtype 관계가 성립하지 않으면 그 generic type을 Invarinace(무공변, 불변성) 이라 한다.  
> List<T>에서 type argument T가 서로 다르면 subtype 관계가 성립하지 않는다.  
이 때, List는 T에 대해 무공변이다.  

type argument 간의 subtype 관계가 성립하고,  
이 subtype 관계가 인스턴스 타입 간의 관계로 이어지는 경우, Covariance(공변적) 이라 한다.  
> B가 A의 subtype일 때, List<B>는 List<A>의 subtype이다.  
이 때, List는 type argument T에 대해 공변적이다.  

#### In/Out  
- T : 별도의 wildcard 정의 없이 read/write.  
- in T : Java의 ? super T. input의 약자이며 write only.  
Kotlin은 기본적으로 null을 허용하지 않기 때문에, add(null)을 할 수 없다.  
- out T : Java의 ? extends T. output의 약자이며 read only.  
Java와 달리 add 자체가 불가능하며, add(null)도 오류를 발생시킨다.  

#### Type Parameter Constraints  
- Java는 extends나 super를 사용하여 사용할 타입의 범위를 제한할 수 있다.  
Kotlin은 : 를 사용하여 타입의 범위를 제한할 수 있다.  
> Java: <T extends Number> T sum(List<T> list)  
  Kotlin: fun <T: Number> List<T>.sum():T  

- 2개 이상의 제약을 걸어야 하는 경우, where을 사용한다.  
이 때의 타입은 나열된 조건 타입들을 전부 만족해야 한다.  
클래스는 1개의 클래스만 상속받을 수 있으므로 2개 이상의 제약은 1개의 클래스와 1개 이상의 인터페이스가 된다.  
> fun <T> ensureTrailingPeriod(seq: T) where T : CharSequence, T : Appendable {}  

#### NonNull Type Parameter  
Kotlin 타입은 기본적으로 NonNull이지만, Generic 타입은 기본이 Nullable이다.  
NonNull인 타입으로 제한하려면 명시적으로 <T : Any> 로 선언해야 한다.  
<T>만 선언하면 <T: Any?> 와 같다.  

#### Star-projections  
타입을 알 수 없지만, 안전하게 사용하고 싶을 때, generic type의 projection을 정의할 수 있다.  
generic type의 모든 인스턴스들이 정의한 projection의 하위 타입이 될 것이다.  
코틀린에서는 star-projection 이라는 syntax를 제공한다.  
