#### How to upload dSYM  
- 직접 업로드하기  
Window -> Organizer -> 아카이빙 된 파일을 찾아 우클릭 한다.  
-> Show in Finder -> xcarchive 파일을 찾아 우클릭 한다.  
-> 패키지 내용 보기 -> dSYM 파일 압축 후 직접 dashboard에 업로드한다.  
- 터미널 명령어로 업로드하기  
프로젝트 폴더로 이동한다.  
Pods/Fabric/upload-symbols -gsp /path/to/GoogleService-Info.plist  
-p <platform> /path/to/dSYMs  
> platform: 앱의 플랫폼 (ios, appletvos, mac)  

- 그럼에도 누락된 dSYM 파일이 있을 경우  
AppStoreConnect -> 나의앱 -> 활동 내역 -> 해당 빌드버전 -> dSYM 다운로드 클릭  
-> 압축 해제 후 위 터미널 명령어로 업로드  
