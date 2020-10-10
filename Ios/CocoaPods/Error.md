## MacOS Catalina Update Error  
  
  
### 오류 메세지  
/usr/local/bin/pod: bad interpreter: /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/bin/ruby: no such file or directory  
  
### 오류 상황  
Homebrew 기반으로 설치한 경우, 발생하는 오류이다.  
  
### 해결 방법  
1. brew upgrade cocoapods  
2. 또는 소스 컴파일 후 링크 걸어주기  
brew install cocoapods --build-from-source  
brew link --overwrite cocoapods  
  
  
  
## Firebase Integration Error  
  
  
### 오류 상황  
Linker 관련 오류들  
  
### 해결 방법  
Target -> Build Settings -> Other Linker Flags -> ${inherited} 추가  
