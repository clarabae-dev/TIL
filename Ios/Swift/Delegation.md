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
