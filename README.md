# flutter_demo_here

here地图的演示版本

## 创建应用

- 启动VSCode，打开控制面板
- 输入flutter，然后选择Flutter: New Project
- 输入项目名称，然后按回车键
- 指定放置项目的位置，然后按蓝色的确定按钮
- 等待项目创建继续，并显示main.dart文件
  
## 添加地图插件

- 登陆官网(<https://developer.here.com>)
- 找到HERE SDKS FOR ANDROID, IOS AND FLUTTER，下载SDK for Flutter
- 找到heresdk-explore-flutter-{version}.tar.gz，解压并重命名为here_sdk
- 在根目录下新建plugins文件夹，再把here_sdk文件夹放置在这里
- 建议再执行命令flutter pub get
- 打开pubspec.yaml，按如下方式添加引用
  
``` sh
 here_sdk:
    path: plugins/here_sdk
```

## 使用

- 在/android/app/src/main/AndroidManifest.xml中添加如下配置
  
``` sh
<meta-data android:name="com.here.sdk.access_key_id" android:value="YOUR_ACCESS_KEY_ID"/>
<meta-data android:name="com.here.sdk.access_key_secret" android:value="YOUR_ACCESS_KEY_SECRET"/>
```

- /ios/Runner/Info.plist中添加如下配置
  
``` sh
<key>HERECredentials</key>
<dict>
<key>AccessKeyId</key>
    <string>YOUR_ACCESS_KEY_ID</string>
<key>AccessKeySecret</key>
    <string>YOUR_ACCESS_KEY_SECRET</string>
</dict>
```

- 运行
  
``` sh
 flutter run
```

## 发布android的版本

- 已有keystore情况下，创建一个名为/android/key.properties的文件，添加如下配置

``` sh
storePassword=<password from previous step>
keyPassword=<password from previous step>
keyAlias=key
storeFile=</Users/<user name>/key.jks>
```

- 编辑/android/app/build.gradle文件为您的应用配置签名，添加如下配置
  
``` sh
def keystorePropertiesFile = rootProject.file("key.properties")
def keystoreProperties = new Properties()
keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
```

``` sh
signingConfigs {
    release {
        keyAlias keystoreProperties['keyAlias']
        keyPassword keystoreProperties['keyPassword']
        storeFile file(keystoreProperties['storeFile'])
        storePassword keystoreProperties['storePassword']
    }
}
buildTypes {
    release {
        signingConfig signingConfigs.release
    }
}
```

- 打包
  
``` sh
flutter build apk
```

## 发布iOS的版本

- 在Xcode中，在您工程目录下的ios文件夹中打开Runner.xcworkspace
- 选择Product > Scheme > Runner.
- 选择Product > Destination > Generic iOS Device.
- 在Xcode项目导航器中选择 Runner，然后在设置视图边栏中选择选择Runner target
- 在Identity部分中，将Version更新为您希望发布的面向用户的版本号
- 在Identity部分中，将Build标识更新为用于跟踪iTunes Connect上的此版本的唯一版本号，每次上传都需要一个唯一的build号
- 打包
  
``` sh
flutter build ios
```

## 内部测试版

- android 1.0版
  
``` sh
http://fir.transcodegroup.com/zr94
```

- iOS 1.0版
  
``` sh
http://fir.transcodegroup.com/7vjp
```
