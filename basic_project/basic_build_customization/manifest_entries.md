# Manifest 属性
通过 DSL 可以配置以下 manifest 属性：

* minSdkVersion
* targetSdkVersion
* versionCode
* versionName
* applicationId（有效的包名--查看 [ApplicationId 与 PackageName](../../appendix/applicationid_versus_packagename.md) 了解更多信息）
* testApplicationId（测试应用的包名）
* testInstrumentationRunner（Instrumentation 的 test runner）

例子：

``` Groovy
android {
   	compileSdkVersion 19
   	buildToolsVersion "19.0.0"

   	defaultConfig {
       	versionCode 12
       	versionName "2.0"
       	minSdkVersion 16
       	targetSdkVersion 16
   	}
}
```

在 **<font color='green'>android</font>** 元素中的 **<font color='green'>defaultConfig</font>** 定义了所有的配置。

Android Plugin 的早期版本使用`packageName`来配置 manifest 的 `packageName` 属性。从 0.11.0 版本开始，你应该在 `build.gradle` 中使用 `applicationId` 来配置 manifest 的 `packageName` 属性。这是为了消除应用程序的 packageName（程序的 ID ）和 java 包名所引起的歧义。

在构建文件中定义的强大之处在于它是动态的。 例如，可以从一个文件中或者其它自定义的逻辑代码中读取版本信息：

``` Groovy

def computeVersionName() {
    ...
}

android {
    compileSdkVersion 19
    buildToolsVersion "19.0.0"

    defaultConfig {
        versionCode 12
        versionName computeVersionName()
        minSdkVersion 16
        targetSdkVersion 16
    }
}
```

---

> 注意: 不要使用在给定范围内同名的 getter 方法，否则可能引起冲突。例如，在 `defaultConfig{...}` 中调用 `getVersionName()` 将会自动调用 defaultConfig.getVersionName() 方法，你自定义的 getVersionName() 方法就不会被调用。

---

如果没有使用 DSL 来设置属性的值，则会使用默认的属性值。下表是可能用到的值：

属性名| 在 DSL 对象中的默认值 | 默认值
----|------|----
**<font color='green'>versionCode</font>**|-1| 从 manifest 中读取
**<font color='green'>versionName</font>**|null| 从 manifest 中读取
**<font color='green'>minSdkVersion</font>**|-1| 从 manifest 中读取
**<font color='green'>targetSdkVersion</font>**|-1| 从 manifest 中读取
**<font color='green'>applicationId</font>**|null| 从 manifest 中读取
**<font color='green'>testApplicationId</font>**|null|applicationId + “.test”
**<font color='green'>testInstrumentationRunner</font>**|null|android.test.InstrumentationTestRunner
**<font color='green'>signingConfig</font>**|null|null
**<font color='green'>proguardFile</font>**|N/A (set only)|N/A (set only)
**<font color='green'>proguardFiles</font>**|N/A (set only)|N/A (set only)

如果你在构建脚本中使用代码获取这些属性，那么第二列的值将非常重要。例如，你可能会写：

``` Groovy
if (android.defaultConfig.testInstrumentationRunner == null) {
    // assign a better default...
}
```

如果值一直为 `null`，那么在构建的时候将被替换成第 3 列的默认值，但是在 DSL 中没有包含该值，所以你无法查询到该值。
除非真的有必要去设置属性的值，否则错误的值可能会阻碍 Gradle 解析应用的 manifest 文件。
