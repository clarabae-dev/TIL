#### Install
1. Local  
- brew install jenkins  
> jenkins-lts : Long-Term Support release  
  jenkins : Weekly releases deliver bug fixes and new features rapidly to users  

2. AWS  
- sudo yum update -y  
- sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo  
> jenkins repo 추가  

- sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key  
> jenkins 저장소 키 등록  

- sudo yum install jenkins -y  
- sudo service jenkins start  
- ec2 보안그룹 8080 포트 추가  

#### Start Service
- jenkins  
> 서비스를 최초 실행하면, 어드민 패스워드와 저장된 위치가 나온다.  

- brew services start jenkins  
> brew 명령어로 서비스를 실행하면 어드민 패스워드와 저장된 위치가 나오지 않음.  

- localhost:8080  
- cat $Home/.jenkins/secrets/initialAdminPassword  
- input admin password -> install plugins -> create admim user -> instance configuration   

#### Remove
- brew services list  
- brew services stop jenkins-lts(또는 jenkins)  
- brew remove jenkins  
- rm -rfv $HOME/.jenkins  

#### Gitlab 연동
1. Jenkins 환경설정  
- Jenkins 관리 -> Global Tool Configuration -> jdk, git, gradle 경로 설정  
> Gradle Wrapper를 사용한다면 경로를 명시할 필요없음  

  Invoke Gradle: 설치된 gradle 버전으로 빌드 ex) gradle clean build  
  Gradle Wrapper: jenkins workspace의 해당 아이템의 gradlew로 빌드 ex) ~/.jenkins/workspace/{new-item}/gradlew clean build  

2. Jenkins Project 생성  
- 새로운 Item -> Freestyle project  
- 소스코드 관리 -> Git -> Repositories -> Repository URL -> Gitlab 프로젝트 Url 입력  
- Add Credentials  
  Kind: Username with password  
  Username: Gitlab 계정 ID  
  Password: Gitlab 계정 Password  
  ID: Jenkins가 Credentials를 구별하기 위한 식별자  
- 빌드 유발 -> Build when a change is pushed to GitLab. -> GitLab webhook URL(= Jenkins EndPoint) 복사  
- 빌드 유발 -> 고급 -> Secret token -> Generate  
> Jenkins에 build 요청을 위한 webhook을 보낼 수 있는 권한 생성  

- Build -> Invoke Gradle script -> Use Gradle Wrapper -> Make gradlew executable -> Tasks  
> Make gradlew executable : jenkins가 gradlew를 실행할 수 있도록 권한을 자동으로 변경해준다. 체크하지 않으면 권한 에러 발생.     
> Tasks : Build시 사용될 gradle task를 입력  

3. Gitlab Webhook 설정  
- Settings -> Integrations  
  URL: 빌드 유발에서 복사해두었던 GitLab webhook URL  
  Secret Token: 빌드 유발에서 복사해두었던 Secret Token  
- Add Webhook -> Test -> HTTP 200이 나타나면 정상 작동한 것.  

#### Github 연동  
1. Github Access Token 발급  
- Profile -> Settings -> Developer Settings -> Personal access tokens -> Generate new token  
- Note에 token의 용도 입력: jenkins  
- jenkins에서 필요로 하는 github permission scope 설정  
https://support.cloudbees.com/hc/en-us/articles/234710368-GitHub-Permissions-and-API-token-Scopes-for-Jenkins#githubapitokenscopesforjenkins  
- Generate Token -> 꼭 Token Copy할 것. 다시 확인할 수 없음.  

2. Jenkins - Github 연결  
- Jenkins 관리 -> 시스템 설정  
- GitHub -> Add GitHub Server  
- Add Credentials  
  Kind : Secret text  
  Secret : Github에서 생성한 Access Token  
  ID : credential 식별자  
- Test Connection -> 'Credentials verified for user ~'  
- Jenkins Location -> Jenkins URL -> 외부 접근(Github)을 위해 pulibc ip 변경  

3. Jenkins Project 생성  
- 새로운 Item -> Freestyle project  
- General -> Github project -> Project url -> Github 프로젝트 Url 입력  
- 소스코드 관리 -> Repositories -> Repository URL -> Github 프로젝트 Url 입력  
- Add Credentials  
  Kind : Username with password  
  Username : Github 계정 ID  
  Password : Github 계정 Password  
- 빌드 유발 -> Github hook trigger for GITScm polling  
- Build -> Invoke Gradle script -> Use Gradle Wrapper -> Make gradlew executable -> Tasks  

4. Jenkins Build Test
- Build Now  
> 연결된 Github project를 받아와 Tasks에 설정한 gradle task를 수행  
  빌드 결과물 위치 : ~/.jenkins/workspace/"project"/build/libs  
