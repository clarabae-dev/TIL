#### Social Api Release Key
keytool -exportcert -alias <release_key_alias> -keystore  
<key_store_path>/key_name.jks | openssl sha1 -binary | openssl base64  
>jks 확장자를 꼭 붙여주어야 cmd에서 key hash 값을 확인하면서 경로에 파일도 생성된다.  
