#### How to add to project  
- .otf or .ttf 파일을 Xcode 프로젝트에 import.  
*첨부할 때 타겟을 해당 프로젝트로 체크하였는지 확인.*  
- Build Phases -> Copy Bundle Resources 에서 폰트가 정상적으로 첨부되어있는지 확인.  
- info.plist -> Fonts provided by applications 항목 추가  
-> 하위에 (Font Name).otf 형식으로 추가.  
