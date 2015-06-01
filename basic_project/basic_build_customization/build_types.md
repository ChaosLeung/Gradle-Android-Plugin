# 构建类型

默认情况下，Android Plugin 会自动给项目构建 debug 和 release 版本。两个版本的区别在于能否在安全设备上调试，以及 APK 如何签名。

debug 版采用通用的 `name/password` 对来自动创建的密钥证书进行签名（为了防止在构建过程中出现认证请求）。release 版在构建过程中不进行签名，需要稍后再进行签名。

这些配置是通过 **<font color='green'>BuildType</font>** 对象来完成的。默认情况下，两个实例都会被创建，分别是 **<font color='green'>debug</font>** 和 **<font color='green'>release</font>**

Android plugin 允许像创建其他*构建类型*一样定制这两个实例。可以在 **<font color='green'>buildTypes</font>** 的 DSL 容器中完成：

``` Groovy
android {
    buildTypes {
        debug {
            applicationIdSuffix ".debug"
        }

        jnidebug.initWith(buildTypes.debug)
        jnidebug {
            packageNameSuffix ".jnidebug"
            jnidebugBuild true
        }
    }
}
```

上面的代码片段实现了以下功能：

* 配置默认的 **<font color='green'>debug</font>** 构建类型:
  * 设置包名为`<app appliationId>`.debug，以便能够在同一个设备上安装 *debug* 和 *release* 版的 apk
* 创建了名为 **<font color='green'>jnidebug</font>** 的新 *BuildType*，并且用 **<font color='green'>debug</font>** 构建类型的默认配置来初始化自身。
* 继续配置 **<font color='green'>jnidebug</font>**，可以构建 JNI 组件，并添加了不一样的包名后缀。

创建一个*新的构建类型*就是简单的在 **<font color='green'>buildTypes</font>** 标签下添加一个新的元素，并且通过调用 **<font color='green'>initWith()</font>** 或者直接使用闭包来配置它。

以下是一些可能使用到的属性和默认值：

 属性名	 |debug 类型的默认值	 |release 或其他类型默认值
 ------------- |:-------------:| ----:
 **<font color='green'>debuggable</font>**|true|false
 **<font color='green'>jniDebugBuild</font>**|false|false
 **<font color='green'>renderscriptDebugBuild</font>**|false|false
 **<font color='green'>renderscriptOptimLevel</font>**|3|3
 **<font color='green'>applicationIdSuffix</font>**|null|null
 **<font color='green'>versionNameSuffix</font>**|null|null
 **<font color='green'>signingConfig</font>** |android.signingConfigs.debug|null
 **<font color='green'>zipAlign</font>**|false|true
 **<font color='green'>runProguard</font>**|false|false
 **<font color='green'>proguardFile</font>**|N/A (set only)|N/A (set only)
 **<font color='green'>proguardFiles</font>**|N/A (set only)|N/A (set only)

除了以上属性外，*Build Types* 还会受项目源码和资源影响。  
对于每一个 Build Type 都会自动创建一个匹配的 *sourceSet*。默认的路径为：

``` Grovvy
src/&lt;buildtypename>/
```

这意味着 *BuildType* 名称不能是 *main* 或者 *androidTest*（因为这两个是由 plugin 强制实现的），并且他们都必须是唯一的。

跟其他 sourceSet 设置一样，Build Type 的 source set 路径也可以重新定向：

``` Grovvy
android {
    sourceSets.jnidebug.setRoot('foo/jnidebug')
}
```

另外，每一个 *Build Type* 都会创建一个新的 `assemble<BuildTypeName>` 任务。

**<font color='green'>assembleDebug</font>** 和 **<font color='green'>assembleRelease</font>** 在上面已经提到过，这里要讲的是它们从哪被创建。当 **<font color='green'>debug</font>** 和 **<font color='green'>release</font>** 构建类型被预创建的时候，它们的 tasks 就会自动创建。

上面提到的 *build.gradle* 代码片段中也会实现 **<font color='green'>assembleJnidebug</font>** task，并且 **<font color='green'>assemble</font>** 会像依赖于 **<font color='green'>assembleDebug</font>** 和 **<font color='green'>assembleRelease</font>** 一样依赖于 **<font color='green'>assembleJnidebug</font>**。

提示：你可以在终端下输入 `gradle aJ` 去运行 **<font color='green'>assembleJnidebug</font>** task。

可能会使用到的情况：

* debug 模式下才用到的权限
* 自定义的 debug 实现
* 为 debug 模式使用不同的资源（例如，当资源的值由绑定的证书决定）

*BuildType* 的代码和资源通过以下方式被使用：

* manifest 将被混合进 app 的 manifest
* 代码只是换了一个资源文件夹
* 资源将叠加到 main 的资源中，并替换已存在的资源。


