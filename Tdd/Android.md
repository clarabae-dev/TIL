### Android Test
Local Unit Test: JVM 위에서 test를 수행.  
Instrumented Unit Test: Android System을 요구하는 test를 수행.  

- InstrumentationRegistry
애플리케이션이 보유한 시스템 리소스(Context 등)를 참조하고 있는 registry.  
- Instrumentation Class  
애플리케이션과 시스템의 상호작용을 모니터링할 수 있다.  
Instrumentation 객체는 애플리케이션의 구성요소 이전에 인스턴스화된다.  
