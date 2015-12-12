# Manifest 属性
通过 DSL 可以配置以下 manifest 属性：

* minSdkVersion
* targetSdkVersion
* versionCode
* versionName
* applicationId（有效的包名--查看 [ApplicationId 与 PackageName][1] 了解更多信息）
* testApplicationId（测试应用的包名）
* testInstrumentationRunner

例子：

``` Groovy
android {
   	compileSdkVersion 23
   	buildToolsVersion "23.0.1"

   	defaultConfig {
       	versionCode 12
       	versionName "2.0"
       	minSdkVersion 16
       	targetSdkVersion 23
   	}
}
```

可查看 [Android Plugin DSL Reference][2] 了解可配置的属性以及它们的默认值。

在构建文件中定义的强大之处在于它是动态的。例如，可以从一个文件中或者其它自定义的逻辑代码中读取版本信息：

``` Groovy
def computeVersionName() {
    ...
}

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.1"

    defaultConfig {
        versionCode 12
        versionName computeVersionName()
        minSdkVersion 16
        targetSdkVersion 23
    }
}
```

> 注意: 不要使用在给定范围内同名的 getter 方法，否则可能引起冲突。例如，在 **<font color='green'>defaultConfig{...}</font>** 中调用 **<font color='green'>getVersionName()</font>** 将会自动调用 **<font color='green'>defaultConfig.getVersionName()</font>** 方法，你自定义的 **<font color='green'>getVersionName()</font>** 方法就不会被调用。

[1]: ../../appendix/applicationid_versus_packagename.md
[2]: http://google.github.io/android-gradle-dsl/current/