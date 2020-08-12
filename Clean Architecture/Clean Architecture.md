#### Conception  
소프트웨어를 목적에 따라 계층을 분리한다. 분리하는 이유는 다음의 이점들을 얻기 위해서 이다.  
1. Independent of Frameworks  
소프트웨어는 다른 프레임워크/라이브러리에 의존하지 않아도 된다.  
2. Testable  
UI, DB, Server 또는 기타 외부 요소와 관계없이 비즈니스 로직을 테스트할 수 있다.  
3. Independent of UI  
비즈니스 로직 또는 시스템 변경이 없어도 UI를 쉽게 변경할 수 있다.  
4. Independent of Database  
비즈니스 로직을 DB와 분리한다.  
5. Indenpendent of any external agency  
비즈니스 로직은 그 어떤 외부에 대해서 알지 못한다.  
  
#### Layers  
1. Domain Layer  
Entities(Model) + Use Cases(business logic) + Repository Interfaces(protocols)  
다른 Layer에 어떠한 영향도 받지 않는다. 재사용될 수 있는 Layer이다. 비즈니스 로직을 담고있다.  
2. Presentation Layer  
Presenters(ViewModels) + UI(UIViewControllers or SwiftUI Views)  
3. Data Layer  
Repository Implementations + Data Sources  
Repository는 Data Sources(Local DB 또는 Remote API)로부터 데이터를 처리한다.  
Data Layer는 API 응답으로 받은 JSON Data를 Domain Layer에 있는 모델로 변환한다. 그래서 Data Layer는 Domain Layer를 의존한다.  
  
#### Clean Architecture + MVVM  
1. Data Flow  
- View는 ViewModel의 메소드를 호출한다.(ViewController는 ViewModel을 가지고 있다.)  
- ViewModel은 UseCase를 실행한다.(ViewModel은 UseCase를 가지고 있다.)  
- Use Case는 Repository로부터 데이터를 조합한다.
- 각각의 Repository는 Remote Data(Network) or Persistent DB Storage Source or In-memory Data(Remote or Cached)로부터 데이터를 가져온다.  
- 데이터는 적절한 모델로 변환되어 다시 View(UI)로 넘어오고, 새로운 화면으로 업데이트 된다.  
  (뷰컨트롤러의 바인드 함수에서 뷰모델의 요소들을 옵져빙해서 화면을 갱신한다.)  