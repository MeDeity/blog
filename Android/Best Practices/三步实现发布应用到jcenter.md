本文的主角是[novoda/bintray-release](https://github.com/novoda/bintray-release)

1.在项目级的build.gradle中加入
```
dependencies {
        //截止目前的版本是 0.9.1
        classpath 'com.novoda:bintray-release:0.9.1'
    }
```
2.在lib库中build.gradle中加入以下内容
```
publish {
    userOrg = 'lastdeity'//bintray.com用户名
    repoName = 'Android-lib'//默认的仓库名称,请确保jcenter中存在以该名称命名的仓库
    groupId = 'com.mengya'//组织ID,随你喜欢
    artifactId = 'smsobserver'//项目名称
    publishVersion = '1.0.0'//版本号
    desc = 'a library for hook sms'//描述
    website = 'https://github.com/MeDeity/SmsObserverForAndroid'//项目地址
}
```

3.执行以下命令
```
# 请自行更改 BINTRAY_USERNAME 和 BINTRAY_KEY
gradlew clean build bintrayUpload -PbintrayUser=BINTRAY_USERNAME -PbintrayKey=BINTRAY_KEY -PdryRun=false
```