## Conception  
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
  
![Alt text](https://blog.kakaocdn.net/dn/MQ1R1/btqFKDrPxtp/pjv2GVcCJ7ubcfjq8ZxQkK/img.png)  
  
  
  
  
## Layers  
  
  
### Domain Layer  
1. Entities(Model) + Use Cases(Interactor) + Repository Interfaces(protocols)  
2. 다른 Layer에 어떠한 영향도 받지 않는다. 재사용될 수 있는 Layer이다. 비즈니스 로직과 어플리케이션 로직을 담고있다.  
3. 다른 Layer에 어떠한 영향도 받지 않기 때문에 Presentation Layer에 의존하지 않으며, 
Data Layer는 직접 의존하지 않고 Dependency Inversion Principle을 사용해 Data Layer의 Repository 영역을 추상화한 protocol들을 가진다.  
Presentation Layer는 UseCase를 통해 데이터를 요청하고 응답을 받는다.  
*Use Case: 1개 이상의 Repository를 받아 비즈니스 로직을 처리하는 부분이다.  
1. 하나의 유저 행동에 대한 비즈니스 로직을 가지고 있다. 1개의 유저 행동에 따른 1개의 로직만을 반환한다.  
2. Presentation Layer와 Data Layer를 연결해주는 매개체이다.  
3. ViewModel의 요청을 파라미터로 넘겨받고, 데이터 호출을 한 뒤, 결과값을 뷰모델에 반환해준다.  

### Presentation Layer  
Presenters(ViewModels) + UI(UIViewControllers or SwiftUI Views)  
Presentation Layer는 Domain Layer에만 의존한다.  
ViewModel에는 UIKit, SwiftUI 등 UI 프레임워크를 import 하지 않는다.  
그래야 UIKit을 SwiftUI로 전환하는 등 리펙토링이나 재사용 측면에 있어서 쉽게 코드를 수정할 수 있다.  
View는 비즈니스 로직이나 어플리케이션 로직에 접근할 수 없다. ViewModel만이 접근할 수 있다.  

### Data Layer  
Repository Implementations + Data Sources  
Repository는 Data Sources(Local DB 또는 Remote API)로부터 데이터를 처리한다.  
Data Layer는 API 응답으로 받은 JSON Data를 Domain Layer에 있는 모델로 변환한다. 그래서 Data Layer는 Domain Layer를 의존한다.  
  
## With MVVM  
  
  
### Data Flow  
1. View는 ViewModel의 메소드를 호출한다.(ViewController는 ViewModel을 가지고 있다.)  
2. ViewModel은 UseCase를 실행한다.(ViewModel은 UseCase를 가지고 있다.)  
3. Use Case는 Repository로부터 데이터를 조합한다.
4. 각각의 Repository는 Remote Data(Network) or Persistent DB Storage Source or In-memory Data(Remote or Cached)로부터 데이터를 가져온다.  
5. 데이터는 적절한 모델로 변환되어 다시 View(UI)로 넘어오고, 새로운 화면으로 업데이트 된다.  
  (뷰컨트롤러의 바인드 함수에서 뷰모델의 요소들을 옵져빙해서 화면을 갱신한다.)  
  
### MVVM with Clean Architecture vs MVVM without Clean Architecture  
MVVM은 UI와 비즈니스 로직을 분리하기 위한 디자인 패턴이다.  
Clean Architecture는 더 나아가 소프트웨어의 계층 분리를 통해 테스트 용이성, 코드 재사용성, 리펙토링 용이성을 추구한다.  
  
  
  
## Repository Pattern  
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