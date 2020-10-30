## Xcode Build Error  
  
  
### Multiple commands produce '.../info.plist'  

#### background  
info.plist 파일을 루트 폴더의 하위 폴더로 옮겼을 때 발생하였다.  
  
#### solution  
1. Target -> Build Phases -> Copy Bundle Resources -> info.plist 파일 제거  
2. Clean Build Folder, command + shift + k  
3. 재빌드하면, 다음과 같은 오류가 발생한다. Build input file cannot be found '.../info.plist'  
적힌 경로를 확인하면 옮겨놓은 info.plist 파일이 루트 폴더에 위치하는 것으로 되어있다. 경로를 수정해준다.  
4. Target -> Build Settings -> search info.plist -> Packaging -> info.plist 경로 수정  