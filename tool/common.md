mac命令

### 获取默认debug签名SHA1值方法

	keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android  

### 获取正式签名的SHA1值方法  

    keytool -v -list -keystore 将签名拖进来 回车键 输入密码  

### Update something  
