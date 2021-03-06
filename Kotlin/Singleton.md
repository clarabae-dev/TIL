#### Basic Singleton Pattern  
object Singleton  

- object  
object로 선언한 클래스는 함수, 프로퍼티, init 메소드를 가질 수 있다.  
constructor 메소드는 사용할 수 없으며, init 메소드를 활용해 모든 초기화 작업을 수행해야 한다.  
object로 선언한 클래스는 처음 호출하는 시점에 인스턴스화 된다.  

#### Singleton Pattern In Class  
class ToDoApplication : Application() {  
    init {  
      context = this  
    }  
    companion object {  
      lateinit var context: ToDoApplication  
      private set  
    }  
    override fun onCreate() {  
      super.onCreate()  
    }  
}  

- companion object  
클래스에 argument가 필요한 경우, companion object를 활용해 싱글턴을 만들 수 있다.  
모든 클래스는 companion object를 구현할 수 있다. Java의 static처럼 쓰인다.  
그러나 inner로 선언된 companion object의 경우 static이라기 보다 outer class의 인스턴스를 싱글턴으로 쓸 수 있게 해준다.  
그래서 일반적인 inner companion object로 데이터 바인딩 어댑터 함수를 작성하면 DataBinding code generator가 찾지 못한다.  
inner companion object를 실제 static처럼 쓰기 위해서는 @JvmStatic annotation이 필요하다.  

- lateinit  
프로퍼티가 클래스 초기화 시점에는 값을 가지고 있지 않지만, 사용되기 전 값이 할당된다.  
값이 할당되지 않으면 Exception을 반환한다.  

- private set  
외부 클래스가 프로퍼티에 값을 할당할 수 없다.
