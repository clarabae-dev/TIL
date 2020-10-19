## Behavior Driven Development  
BDD는 행위에 초점을 맞춰 자연스럽고 인간이 읽을 수 있는 언어로 테스트 코드를 작성할 것을 권장한다.  
BDD는 Arrange - Act - Assert 라는 구조화된 테스트 작성법을 정의한다.  
1. given: 몇 가지 전제 조건 (Arrange)  
2. when: 행위의 발생 (Act)  
3. then: 결과 검증 (Assert)  
  
  
### How to use  
가장 일반적인 활용법은 메소드가 반환하는 값으로 stub을 만드는 것이다.  
  
```java
@MockBean  
private StudentRepository studentRepository;  
String givenName = "pei";  
int givenScore = 100;  
given(studentRepository.getStudent(givenName)).willReturn(new Student(givenName, givenScore));  
```  
  
1. should() / should(VerificationMode)  
mock 객체의 활동을 검증하고자 할 때 사용한다.  

```java
then(mock).should().getData(); //getData()를 한번 호출했는지 검증.  
then(mock).should(times(2)).processData(); //processData()를 두번 호출했는지 검증.
```  
  
2. InOrder  
mock 객체의 메소드 호출 순서를 검증하고자 할 때 사용한다.  
  
```java
InOrder inOrder = inOrder(mock);  
then(mock).should(inOrder, times(2)).processData();  
// mock 객체가 processData를 첫번쨰, 두번째 순서로 호출했는지 검증.
```  
  