一、当出现依赖库冲突时,可以使用以下命令查看依赖树:
```
gradlew app:dependencies
```
二、强制指定依赖库版本的版本
在第三方依赖过膨胀的过程中,依赖库冲突的情况非常常见,此时可以使用以下命令强制指定依赖库的版本：
在project级别的build.gradle中
```
allprojects {
    repositories {
        google()
        jcenter()
    }

    configurations.all {
        resolutionStrategy.force 'androidx.arch.core:core-runtime:2.0.1'
        resolutionStrategy.force 'androidx.fragment:fragment:1.1.0-rc04'
        ...
    }
}
```


三、gralde错误信息不够明显是怎么办
例如下面的错误信息.
Error:Executionfailedfortask':test:processDebugManifest'.>Manifest merger failed with multiple errors
然后就没有然后了,没有任何详细信息.这种情况下,就需要使用trace命令打印错误栈了
```
/// processDebugManifest 是编译过程中错误的task名称
gradlew processDebugManifest --stacktrace
```