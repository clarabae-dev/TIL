#### Behavior Driven Development
BDD는 행위에 초점을 맞춰 자연스럽고 인간이 읽을 수 있는 언어로 테스트 코드를 작성할 것을 권장한다.  
BDD는 Arrange - Act - Assert 라는 구조화된 테스트 작성법을 정의한다.  
- given: 몇 가지 전제 조건 (Arrange)
- when: 행위의 발생 (Act)
- then: 결과 검증 (Assert)

#### 활용 예시
가장 일반적인 활용법은 메소드가 반환하는 값으로 stub을 만드는 것이다.  

@MockBean  
private StudentRepository studentRepository;  
String givenName = "pei";  
int givenScore = 100;  
given(studentRepository.getStudent(givenName)).willReturn(new Student(givenName, givenScore));  
