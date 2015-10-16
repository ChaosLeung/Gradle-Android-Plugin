# 构建文件示例
一个纯 Java 的 Gradle 项目的 build.gradle 文件可以简单到只包含以下内容:

``` groovy
apply plugin: 'java'
```

这里引入了 Gradle 的 Java 插件，该插件提供了所有构建和测试 Java 应用程序所需的东西。

最简单的 Android Gradle 项目的 build.gradle：

``` groovy
buildscript {
    repositories {
        mavenCentral()
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:1.3.0'
    }
}

apply plugin: 'com.android.application'

android {
    compileSdkVersion 19
    buildToolsVersion "19.0.0"
}
```

<font color='red'>译者注：</font>目前 Gradle Tools 版本为 1.3.0 （2015.10.16）

上述内容包含了 Android 构建文件的 3 个主要部分：

**<font color='green'>buildscript { ... }</font>** 配置了驱动构建的代码.  
在这部分，声明了项目使用 Maven 仓库，并且声明了一个 Maven 文件的 classpath。  
该文件声明了项目的 Android Gradle 插件版本为 1.3.0。

---

> **注意**：这里的配置只影响了构建过程的代码，而不是整个工程的代码.工程本身需要声明它自己的仓库和依赖.这个后面会提到.

---

接下来，跟前面提到的 Java 插件一样添加了 **<font color='green'>android</font>** 插件.

最后，**<font color='green'>android { ... }</font>** 配置了所有 android 构建所需的参数，这也是 Android DSL 的入口点。  
默认情况下，只有 **<font color='green'>compileSdkVersion</font>** 和 **<font color='green'>buildtoolsVersion</font>** 这两个属性是必须的。  
**<font color='green'>compileSdkVersion</font>** 属性相当于旧构建系统中 `project.properites` 文件中的 **<font color='green'>target</font>** 属性。这个新的属性可以跟旧的 **<font color='green'>target</font>** 属性一样指定一个 `int` 或者 `String` 类型的值。

---

> **重要：**  **<font color='green'>android</font>** 插件不能与 **<font color='green'>java</font>** 插件同时使用，否则会导致构建错误.

---

---

> **注意：**  你需要在相同路径下添加一个 *local.properties* 文件，并使用 **<font color='green'>sdk.dir</font>** 属性来设置 SDK 路径。或通过设置 **<font color='green'>ANDROID_HOME</font>** 环境变量来设置 SDK 路径，这两种方式没有什么不同，根据你自己的喜好选择其中一种设置。
___






