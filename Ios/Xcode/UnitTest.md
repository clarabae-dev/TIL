## TDD in iOS  
1. Unit Test  
Unit Test는 소프트웨어 테스트 방법으로 소스 코드의 개별 유닛들이 사용에 적합한지 확인하기 위해 테스트 한다.  
Unit Test를 통해 비즈니스 로직, 핵심 기능 등이 의도한대로 동작하는지 검증할 수 있다.  
2. UI Test  
UI 관련부를 테스트한다.  
  
  
### 기존 프로젝트에 테스트 추가  
1. 좌측 네비게이터에서 프로젝트를 선택한다.  
2. 타겟 목록 최하단의 + 버튼 클릭.  
3. iOS 탭에서 Unit Testing Bundle 또는 UI Testing Bundle을 선택한다.  
4. 타겟명 지정 후, Done 클릭.  
  
### Unit Test  
1. setUpWithError  
- Xcode 11.4 이후부터 setUp 대신 적용되는 메소드이다. 기존 setUp도 사용할 수 있다.  
- 테스트 메소드가 실행되기 전 호출된다.  
- 호출순서: setUpWithError -> setUp -> tearDown -> tearDownWithError  
- 이 부분에 작성한 코드에서 오류가 발생할 경우, 해당 테스트는 스킵되고, tearDownWithError를 호출한다.  
2. tearDownWithError  
- Xcode 11.4 이후부터 tearDown 대신 적용되는 메소드이다. 기존 tearDown도 사용할 수 있다.  
- 테스트 메소드가 실행된 후 호출된다.  
3. @testable import  
Xcode에서 생성한 타겟들은 별도의 모듈로 처리된다. 각 타겟의 코드들이 public, open으로 선언되지 않은 이상 다른 타겟에서 해당 소스에 접근할 수 없다.  
Swift의 기본 access level은 internal이기 때문에 테스트 타겟은 앱 타겟의 소스 코드에 접근할 수 없다.  
  
  
  
출처:  
https://stackoverflow.com/a/6866120  
https://zeddios.tistory.com/991  