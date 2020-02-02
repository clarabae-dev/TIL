1. Modifications to the layout engine must not be performed  
from a background thread after it has been accessed from the main thread.  
- Main Thread가 아닌 곳에서 UI를 수정하는 경우  
- 위의 경우에 해당하는 곳을 찾아서 DispatchQueue.main.async{} 등으로 감싸준다.  
