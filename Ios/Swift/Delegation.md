#### Delegate Pattern
- delegate, 위임하다, 대표하다  
- 어떤 객체가 해야하는 일을 대신 처리한다.
- 객체간 추상화를 통해 결합도를 최소화할 수 있다.(객체가 해야할 일이 몰려있지 않기 때문)
- MVVM에서 대신 처리하는 객체는 ViewController가 될 수 있다.  
뷰에 변화가 생겼을 때, 뷰모델은 delegate를 통해 모델에게 뷰의 변화를 알린다.  

#### 활용 예시
delegate pattern은 protocol로 구현되어 있다. protocol은 서로간에 '~ 경우에는 이러이러하게 행동하자' 라는 약속과 같다.  
protocol은 상호간 약속을 정의만 해준다. 직접 구현은 해당 protocol을 준수하겠노라고 채택한 곳에서 한다.  
delegate의 활용 과정은 다음과 같다. protocol 채택 -> 위임자 지정 -> protocol 구현
  
```swift
class ViewController: UIViewController, UITextFieldDelegate { // 1. ViewController는 UITextFieldDelegate를 준수하겠노라고 채택한다.  
        
    @IBOutlet weak var textField: UITextField!  
    @IBOutlet weak var label: UILabel!  
    
    override func viewDidLoad() {  
        super.viewDidLoad()  
        textField.delegate = self  
        // 2. UITextFieldDelegate를 채택한 곳들 중에서 textField를 대신해줄 위임자를 지정한다.  
        // 이경우, self 즉, ViewController 자신이다. 이제 ViewController는 textField에 이벤트가 발생하면 UITextFieldDelegate라는 프로토콜에 따라 textField 대신 행동하게 된다.  
    }  
    
    func textFieldShouldReturn(_ textField: UITextField) -> Bool { // 3. 프로토콜에 따라 동작을 대신 해줄 함수를 불러와 직접 구현한다.  
        label.text = textField.text  
        return true  
    }  
}  
```

#### 유사 패턴
- 유사패턴: Java8 인터페이스 default 메서드
인터페이스가 default 키워드로 선언되면 메소드를 구현할 수 있다. 또한 이를 구현하는 클래스는 default 메소드를 오버라이딩 할 수 있다.  
인터페이스가 변경되면, 인터페이스를 구현하는 모든 클래스들이 해당 메소드를 구현해야 하는 문제가 있다.  
이런 문제를 해결하기 위하여 인터페이스에서 default 메소드를 구현해 놓을 수 있도록 하였다.  
  
```swift
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
```