## How to obtain certificate and key  
APNs 인증서를 예로 인증서와 키를 발급받는 방법을 살펴본다.  
  
  
### Process  
1. Apple Developer -> Certificates, Identifiers & Profiles  
2. Certificates + 버튼 클릭  
3. Services -> Apple Push Notification service SSL 선택 -> Continue  
- Sandbox: 개발용 또는 테스트용으로 개발할 때 활용할 수 있다.  
- Sandbox & Production: 프로덕트와 개발용 모두 활용할 수 있다.  
4. 인증서를 적용할, 푸시 알림을 적용할 App ID 선택 -> Continue  
5. Mac에서 발급한 키체인 인증서 업로드  
  
#### 키체인 인증서 생성 방법  
1. 키체인접근 -> 상단 키체인 접근 메뉴 -> 인증서 지원 -> 인증 기관에서 인증서 요청...  
2. Apple ID로 쓰는 이메일 주소 입력 -> 이름(용도) 입력 -> 디스크에 저장됨 선택 -> 계속  
3. 저장할 위치를 지정한 후 저장. 파일명: CertificateSigningRequest.certSigningRequest  
  
  
### Process - 2  
6. [키체인 인증서 생성 방법]에서 발급받은 키체인 인증서를 업로드 -> Continue  
7. 생성된 APNs 인증서를 Download. 파일명: aps.cer  
  
  
  
참고: https://spiralmoon.tistory.com/entry/Apple-Apple-push-notification-service-APNs-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0  