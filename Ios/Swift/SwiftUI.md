1. 새로 추가된 요소  
- SceneDelegate.swift  
SwiftUI를 추가하지 않더라도 iOS13부터 추가된 delegate이다. iPad와 같이 멀티 윈도우를 지원하기 위해 추가되었다.  
동일한 앱을 여러 화면에 띄울 경우, AppDelegate는 앱 전역에서 동작하는데 반해 SceneDelegate는 각 화면의 인스턴스 단위로 동작시킬 수 있다.  

- ContentView.swift  
Simulator를 실행하면 맨 처음 출력되는 SwiftUI View로 SceneDelegate 클래스의 Scene 메서드에 선언되어있다.  
*window.rootViewController = UIHostingController(rootView: contentView)*  
UIHostingController는 SwiftUI View를 인자로 받아 ViewController를 만드는 역할을 한다.  

SwiftUI를 import하여 프레임워크를 가져오고, View를 상속받는 ContentView 구조체가 선언되는 형태이다.  
SwiftUI에서 View는 반드시 body 변수가 있어야하며 최상위 View 역활을 한다.  

ContentView_Previews 구조체는 실제 앱에는 적용되지 않지만 Canvas 기능을 제공하기 위한 preview layout이다.  
Xcode11 버전 이상부터는 상단 Resume 버튼을 눌러 실시간으로 프리뷰를 확인할 수 있으며, 이하 버전은 simulator로 확인 가능하다.  
  
- Preview Content 폴더  
Xcode11 버전부터 Xcode에서 Canvas 기능을 통해 Simulator 없이도 Xcode에서 화면을 미리 볼 수 있게 되었다.
이 Canvas에서 사용되는 데이터들을 위한 Assets.  
  
2. 활용해보기  
- Form Container  
Swift UI에서 최상위 View는 Form 컨테이너로 감싸며 최대 10개의 Child View를 가질 수 있다.  
만약 10개를 초과하게된다면 Group, Stack과 같은 다른 컨테이너로 감싸야 한다.  
Form은 데이터를 그룹화할 수 있도록 해주는 컨테이너이다. SwiftUI는 적절하게 Form 컨테이너를 랜더링하여 보여준다.  
  
- @State  
변수 앞에 @State 키워드를 사용하면 binding 역할을 수행한다.  
ex. TextFiled의 Binding<String>에 @State로 선언한 변수값을 넣으면, TextFiled가 입력받는 텍스트가 @State로 선언한 변수에 저장된다.  
  
- Spacer  
iOS13부터 추가된 구조체로, view layout 내부에 임의의 공간을 부여한다. StackView에서 alignment를 맞추기 위해 활용해 본 적 있다.  