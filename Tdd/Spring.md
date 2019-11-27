#### Test Annotation
1. @MockBean
DI에 Bean으로 등록된 객체들을 mocking.  
2. @Mock
일반 객체들을 mocking.  

#### Spring MVC Test
> 컨트롤러의 역할  
요청 경로  
parameter validation  
dto <-> entity 매핑  
요청한 데이터 얻기  
비즈니스 로직 호출  
이동 화면 제어  

단위 테스트가 필요한 비즈니스 로직을 다루는 것은 컨트롤러의 역할이 아니다.  
따라서 프레임워크 기능까지 통합한 Integration Test의 관점으로 보아야 한다.  
그런데 Integration Test를 진행하려면 웹 어플리케이션을 배포해야 한다.  
MockMvc는 웹 어플리케이션의 배포없이도 Spring MVC의 동작을 재현할 수 있다.
