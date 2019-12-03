#### Key Hash
- Debug Key For Mac  
keytool -importkeystore -srckeystore ~/.android/debug.keystore -destkeystore ~/.android/debug.keystore -deststoretype pkcs12  
- Release Key For Mac  
keytool -exportcert -alias androiddebugkey -keystore <Release Key Store File Path> -storepass android -keypass android | openssl sha1 -binary | openssl base64  
