### 使用flutter_launcher_icons插件快速替换Flutter项目启动图标

插件地址:
[flutter_launcher_icons](https://github.com/fluttercommunity/flutter_launcher_icons)

使用方法(通用版,如不能满足,请看原仓库README.MD)
1. 在pubspec.yaml中新增以下内容:
```
dev_dependencies: 
  flutter_launcher_icons: "^0.7.2"
  
flutter_icons:
  android: true
  ios: true
  image_path: "assets/icon/icon.png"
```
#### android/ios配置项有以下属性
1. true 替换特定平台(android/ios)的启动图标
2. false 本次忽略特定平台(android/ios)的启动图标的生成
3. icon/path/here.png 为特定平台生成指定命名的图标,而不移除原平台的启动图标

#### image_path 
你想用来作为启动图标的的资源文件路径(例如:assets/images/...)

#### image_path_android(可选)
单独为android平台指定启动图标的资源文件路径,可选配置，如果没有，则默认使用image_path的设置

#### image_path_ios(可选)
单独为ios平台指定启动图标的资源文件路径,可选配置，如果没有，则默认使用image_path的设置