#### Social Api Release Key
- Generate Hash Key  
keytool -importkeystore -srckeystore ~/Documents/Bigwalk3.0/bigwalk-android/app/bigwalk_android_key -destkeystore /Users/baeseungmin/Documents/Bigwalk3.0/bigwalk-android/app/bigwalk_android_key  

keytool -exportcert -alias <release_key_alias> -keystore  
<key_store_path>/key_name | openssl sha1 -binary | openssl base64  
>jks 확장자를 꼭 붙여주어야 cmd에서 key hash 값을 확인하면서 경로에 파일도 생성된다.  
