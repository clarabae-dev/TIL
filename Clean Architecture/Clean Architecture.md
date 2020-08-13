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
- Entities(Model) + Use Cases(Interactor) + Repository Interfaces(protocols)  
- 다른 Layer에 어떠한 영향도 받지 않는다. 재사용될 수 있는 Layer이다. 비즈니스 로직을 담고있다.  
- 다른 Layer에 어떠한 영향도 받지 않기 때문에 Data Layer를 직접 의존하지 않고  
Dependency Inversion Principle을 사용해 Data Layer의 Repository 영역을 추상화한 protocol들을 가진다.  
*Use Case: 1개 이상의 Repository를 받아 비즈니스 로직을 처리하는 부분이다.  
Usecase는 하나의 유저 행동에 대한 비즈니스 로직을 가지고 있다. 1개의 유저 행동에 따른 1개의 로직만을 반환한다.*  
2. Presentation Layer  
Presenters(ViewModels) + UI(UIViewControllers or SwiftUI Views)  
Presentation Layer는 Domain Layer에만 의존한다.  
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
  
#### Repository Pattern  
1. Data Layer에서 데이터를 호출하는 영역을 추상화한다.  
- DataSource를 활용해 Remote/Local 영역을 추상화한다.  
- Domain별로 단일 Repository에서 상황에 따라 적절한 DataSource를 호출해 필요한 메소드를 호출한다.  
2. 개인적으로 생각해본 DataSource의 Remote, Local 영역을 class 보다는 struct로 구현하는 것이 좋은 이유  
struct는 value type이고 class는 reference type이다.  
sturct가 value type이라는 뜻은 다음을 의미한다.  
	struct를 할당하거나, 초기화하거나, 함수에 전달할 때, 각 struct instance는 자기만의 데이터를 복사해 가지고 있다.  
	instance를 변경시키더라도, 다른 instance는 변경되지 않는다.  
Remote, Local 영역은 직접 데이터를 호출하고 그 결과를 반환한다. 데이터 값은 언제든 변할 수 있다.  
반면, 여러 곳에서 호출당하는 Repository의 경우, DataSource로부터 반환받은 결과값을 동일하게 유지하기 위해 reference type인 class를 사용한다.  