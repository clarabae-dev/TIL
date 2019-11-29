#### Github 연동하기
1. Github Access Token 발급  
- Profile -> Settings -> Developer Settings -> Personal access tokens -> Generate new token  
- Note에 token의 용도 입력: jenkins  
- jenkins에서 필요로 하는 github permission scope 설정  
https://support.cloudbees.com/hc/en-us/articles/234710368-GitHub-Permissions-and-API-token-Scopes-for-Jenkins#githubapitokenscopesforjenkins  
- Generate Token -> 꼭 Token Copy할 것. 다시 확인할 수 없음.  

2. Jenkins - Github 연결

#### Jenkins 제거
- brew services list  
- brew services stop jenkins-lts(또는 jenkins)  
- brew services uninstall jenkins  
- rm -rfv $HOME/.jenkins  
