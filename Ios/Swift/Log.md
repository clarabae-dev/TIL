### How to print function/line number  
  
```swift
func logMessage(_ message: String,
                  fileName: String = #file,
                  functionName: String = #function,
                  lineNumber: Int = #line,
                  columnNumber: Int = #column) {
    print("🤡🤡🤡 Called by \(fileName) - \(functionName) at line \(lineNumber)[\(columnNumber)]")
}

print(#function)
```  
  
  
  
  
## os_log  
ios 14.0 부터 사용 가능한 Unified Logging System, 통합 로깅 시스템으로 모든 레벨의 시스템에서 메시징을 캡쳐할 수 있게 해준다.  
로그 데이터를 메모리와 디스크의 데이터 저장소에서 모아 메시지를 한데 보여준다.  
  
  
### How to use  
1. import os  
2. call os_log  
  
```swift
os_log("print log", type: .default)
```  

  
### Log Type  
1. Default  
메모리 버퍼에 저장하다가 버퍼가 가득 차면 압축하여 데이터 저장소로 이동된다.  
저장소 할당량도 초과되면 가장 오래된 메세지부터 제거된다.  
주로 failure를 일으킬 수 있는 사항에 대한 정보를 캡쳐한다.  
2. Info  
메모리 버퍼에 저장하다가 버퍼가 가득 차면 제거한다.  
제거되지 않도록 하려면 configuration을 변경하여 데이터 저장소로 이동시킬 수 있다.  
또, faults나 error가 발생할 때에도 데이터 저장소에 캡쳐된다.  
이 레벨의 메세지가 데이터 저장소에 추가되면 할당량을 초과할 때 가장 오래된 메세지부터 제거된다.  
주로 오류 해결에 도움이 될 수 있지만 필수적이지 않은 것을 캡쳐한다.  
3. Debug  
configuration 변경으로 디버그 로깅이 활성화된 경우에만 메모리에 캡쳐한다.  
configuration의 지속성 설정에 따라 메모리에서 제거된다.  
주로 개발 중이나 특정 문제를 해결하는 동안의 유용한 정보를 캡쳐한다.  
4. Error  
항상 데이터 저장소에 저장된다.  
저장소 할당량을 초과하면 가장 오래된 메세지부터 제거된다.  
주로 프로세스 레벨의 오류를 캡쳐한다.  
5. Fault  
항상 데이터 저장소에 저장된다.  
저장소 할당량을 초과하면 가장 오래된 메세지부터 제거된다.  
주로 시스템 레벨이나 다중 프로세스 오류를 캡쳐한다.  
  
### How to See  
콘솔 앱 -> 테스트하는 시뮬레이터 or 디바이스 선택 -> 로그 확인  
  
  
  
참조: https://zeddios.tistory.com/979  