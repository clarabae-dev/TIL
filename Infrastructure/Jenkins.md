#### Install
- brew install jenkins  
> jenkins-lts : Long-Term Support release  
> jenkins : Weekly releases deliver bug fixes and new features rapidly to users  

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

#### Github 연동하기
1. Github Access Token 발급  
- Profile -> Settings -> Developer Settings -> Personal access tokens -> Generate new token  
- Note에 token의 용도 입력: jenkins  
- jenkins에서 필요로 하는 github permission scope 설정  
https://support.cloudbees.com/hc/en-us/articles/234710368-GitHub-Permissions-and-API-token-Scopes-for-Jenkins#githubapitokenscopesforjenkins  
- Generate Token -> 꼭 Token Copy할 것. 다시 확인할 수 없음.  

2. Jenkins - Github 연결  
- Jenkins 관리 -> 시스템 설정 -> GitHub -> Add GitHub Server
