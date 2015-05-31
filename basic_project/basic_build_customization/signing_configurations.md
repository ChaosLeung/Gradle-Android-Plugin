# 签名配置

签名一个应用程序需要以下文件:

* keystore
* keystore密码
* key的别名（alias）
* key密码
* 存储类型

位置，键名，两个密码和存储类型一起组成了这个签名配置（*SigningConfig*）

默认情况下，**<font color='green'>debug</font>** 被配置成使用 debug keystore，debug keystore 使用默认的密码和默认 key 及默认的 key 密码。
debug keystore 的位于 `$HOME/.android/debug.keystore`，如果文件不存在，则会自动创建。

**<font color='green'>debug</font>** *Build Type*（构建类型）会自动使用 **<font color='green'>debug</font>** 的 *SigningConfig*（签名配置）。

可以通过 **<font color='green'>signingConfigs</font>** DSL 容器来创建其他配置或者自定义内建的默认配置:

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
            debuggable true
            jniDebuggable true
            signingConfig signingConfigs.myConfig
        }
    }
}
```

以上代码片段修改了 debug keystore 的路径到项目的根目录下。在这个例子中，这将影响其他用到  **<font color='green'>debug</font>** 构建类型的构建类型。

这里也创建了一个新的 *Single Config*（签名配置）和一个使用这个新签名配置的新的 *Build Type*（构建类型）。

---

> 注意：只有默认路径下的 debug keystore 不存在时才会自动创建。改变 debug keystore 的路径并不会在新路径下自动创建 debug keystore。如果创建不同名的 SigningConfig，并使用默认的 debug keystore 路径，那么还是会在默认路径下创建 debug keystore。换句话说，会不会自动创建是根据 keystore 的路径来判断，而不是配置的名称。

___

>注意：虽然经常使用项目根目录的相对路径作为 keystore 的路径，但是也可以使用绝对路径，尽管这并不推荐（除了自动创建出来的 debug keystore）

___

>**注意：如果将这些文件添加到版本控制，你可能不希望将密码直接写到这些文件。下面的 `Stack Overflow` 链接提供从控制台或者环境变量中获取密码的方法：** <http://stackoverflow.com/questions/18328730/how-to-create-a-release-signed-apk-file-using-gradle>
**我们以后还会在这个指南中添加更多的详细信息。**
