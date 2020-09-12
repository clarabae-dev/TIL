#### 접근제어  
다른 소스 파일이나 모듈에서 특정 코드에 대한 접근을 명시적으로 작성하여 관리하는 것  

#### private extension  
동일한 파일에 있는 extension하려는 같은 대상에 대해서만 접근이 가능하다.  
Ex. 아래 두개의 extension은 모두 EndPoint.swift 파일에 있다.  

``` swift
extension URL {  
    static var recommendations: URL {  
        makeForEndpoint("recommendations")// private extension을 선언한 동일한 대상과 동일한 파일에 있기 때문에 호출이 가능하다.  
    }  
}  
  
private extension URL {  
    static func makeForEndpoint(_ endpoint: String) -> URL {  
        URL(string: "https://api.myapp.com/\(endpoint)")!  
    }  
}  
```
  
ViewController.swift 라는 다른 파일에서 동일한 방식으로 호출하면 다음과 같은 오류가 발생한다.  
  
``` swift
extension URL {  
    static var search: URL {  
        makeForEndpoint("search")// 'makeForEndpoint' is inaccessible due to 'fileprivate' protection level  
    }  
}  
```