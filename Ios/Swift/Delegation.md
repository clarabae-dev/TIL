#### Delegate Pattern
- delegate, 위임하다  
- delegate는 어떤 객체가 해야하는 일을 부분적으로 확장해서 대신 처리한다.
- 객체간 추상화를 통해 결합도를 최소화할 수 있다.
- MVVM에서 대신 처리하는 객체는 ViewController가 될 수 있다.  
뷰에 변화가 생겼을 때, 뷰모델은 delegate를 통해 모델에게 뷰의 변화를 알린다.  

#### 활용 예시
프로토콜이 가장 빈번하게 사용되는 예가 delegate pattern 이다. 클래스 간 이벤트를 알려주기에 효과적인 패턴이기 때문이다.  

protocol ViewModelProtocol {
    var isPaused: Bool { get }
    func pause()
}

class ViewController {
    var delegate: ViewModelProtocol?
    @IBAction func pauseButtonPress(_ sender: AnyObject) {
        delegate?.pause()
    }
}

class ViewModel: ViewModelProtocol {
    var isPaused: Bool
    func pause() {
        self.isPaused = !isPaused
    }
}

#### 유사 패턴
- 유사패턴: Java8 인터페이스 default 메서드
인터페이스가 default 키워드로 선언되면 메소드를 구현할 수 있다. 또한 이를 구현하는 클래스는 default 메소드를 오버라이딩 할 수 있다.  
인터페이스가 변경되면, 인터페이스를 구현하는 모든 클래스들이 해당 메소드를 구현해야 하는 문제가 있다.  
이런 문제를 해결하기 위하여 인터페이스에서 default 메소드를 구현해 놓을 수 있도록 하였다.  

public interface Calculator {  
    public int plus(int i, int j);  
    public int multiple(int i, int j);  
    default int exec(int i, int j){  
        return i + j;  
    }  
}  

public class MyCalculator implements Calculator {  
    @Override  
    public int plus(int i, int j) {  
        return i + j;  
    }  
    @Override  
    public int multiple(int i, int j) {  
        return i * j;  
    }  
}  

public class MyCalculatorExam {  
    public static void main(String[] args){  
        Calculator cal = new MyCalculator();  
        int value = cal.exec(5, 10);  
        System.out.println(value);  
    }  
}  
