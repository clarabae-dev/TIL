## KVC  
프로퍼티에 value를 직접 할당하거나 객체의 setter 메소드를 사용하는 대신, key/keyPaths에 value를 할당하는 단순한 방법을 사용한다.  
key와 value를 사용하므로 이를 Key Value Coding이라 부른다.  
  
  
### NSKeyValueCoding Protocol  
모든 클래스들은 KVC & KVO를 사용하기 위해 반드시 NSKeyValueCoding 프로토콜을 준수해야 한다.  
NSObject는 이 프로토콜을 준수한다. 따라서 Foundation 프레임워크에서 정의하고 NSObject를 상속하는 모든 클래스들은 이 프로토콜을 준수한다.  
  
### Key & KeyPath  
1. Key  
값을 할당하거나 값을 가져오려는 하나의 프로퍼티를 가리키기 때문에 Key의 이름은 프로퍼티의 이름과 같다.  
2. KeyPath  
dot-syntax 형태로 되어있어서 하나의 단어나 문장이 아니다.  
Key-path는 원하는 값/프로퍼티에 도달할 때까지 나타나는 객체의 모든 프로퍼티들을 나타낸다.  
  
  
  
출처: https://medium.com/hackernoon/kvo-kvc-in-swift-12f77300c387  