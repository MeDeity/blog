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
