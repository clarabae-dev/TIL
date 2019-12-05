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
모든 클래스는 companion object를 구현할 수 있다.  
Java의 static과 같다.  

- lateinit  
프로퍼티가 클래스 초기화 시점에는 값을 가지고 있지 않지만, 사용되기 전 값이 할당된다.  
값이 할당되지 않으면 Exception을 반환한다.  

- private set  
외부 클래스가 프로퍼티에 값을 할당할 수 없다.
