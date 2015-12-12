# 签名配置

签名一个应用程序需要以下文件（查看 [Signing Your Application][1] 了解更多 APK 签名的知识）:

* keystore 文件
* keystore 密码
* key alias
* key 密码
* 签名文件的类型

签名文件的路径、类型、key 名及两个密码一起组成了[签名配置][2]。默认情况下，**<font color='green'>debug</font>** 使用 debug keystore，debug keystore 使用默认的 storePassword、keyAlias 及 keyPassword。  
debug keystore 位于 `$HOME/.android/debug.keystore`，如果文件不存在，则会自动创建。**<font color='green'>debug</font>** *Build Type*（构建类型）会自动使用 **<font color='green'>debug</font>** 的 *SigningConfig*（签名配置）。

可以通过 **<font color='green'>signingConfigs</font>** DSL 容器来创建其他配置或者自定义内建（debug、release）的默认配置:

``` Groovy
android {
    signingConfigs {
        debug {
            storeFile file("debug.keystore")
        }

        myConfig {
            storeFile file("other.keystore")
            storePassword "android"
            keyAlias "androiddebugkey"
            keyPassword "android"
        }
    }

    buildTypes {
        foo {
            signingConfig signingConfigs.myConfig
        }
    }
}
```

以上代码片段指定了 debug keystore 的路径在项目根目录下。在该例子中，其他使用了  **<font color='green'>debug</font>** *Build Type* 的 *Build Types* 亦会受到影响。该代码片段同时创建了新的 *Signing Config* 及使用该签名配置的 *Build Type*。

> **注意：**只有默认路径下的 debug keystore 不存在时才会自动创建。改变 debug keystore 的路径并不会在新路径下自动创建 debug keystore。如果创建一个新的 *SigningConfig*，并使用默认的 debug keystore 路径，那么 debug keystore 会自动创建。换句话说，会不会自动创建是根据 keystore 的路径来判断，而不是配置的名称。

> **注意：**虽然我们经常用 keystore 的相对路径，但也可以用绝对路径，尽管这并不推荐（自动创建的 debug keystore 除外）

> **注意：**如果将这些文件添加到版本控制，你可能不希望将密码直接写到这些文件。可查看 [Stack Overflow post][3] 了解如何从控制台或者环境变量中获取密码。

[1]: http://developer.android.com/tools/publishing/app-signing.html
[2]: http://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.SigningConfig.html
[3]: http://stackoverflow.com/questions/18328730/how-to-create-a-release-signed-apk-file-using-gradle