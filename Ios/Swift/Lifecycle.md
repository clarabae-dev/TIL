#### ViewWillAppear가 항상 호출되지 않는 이유  
ViewWillAppear 호출되는 경우:  
ViewController에 view가 view hierarchy에 추가될 것임을 알려줄 때 호출된다.  
이미 view hierarchy에 추가된 경우, ViewWillAppear가 호출되지 않는다.  
