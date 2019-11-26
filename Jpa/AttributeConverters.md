#### 사용 목적
JPA Entity Attribute <-> Database Column Mapping  

#### 활용 예
Enum 타입을 변환할 때 주로 사용하는 중.  
- Enum 클래스 작성.
- AttributeConverter를 implement한 CustomConverter 클래스 작성.  
커스텀 클래스가 항상 적용되는 것을 원할 경우 @Converter(autoApply = true)를 사용.
- Enum attribute에 @Converter(converter = CustomConverter.class) 선언.
