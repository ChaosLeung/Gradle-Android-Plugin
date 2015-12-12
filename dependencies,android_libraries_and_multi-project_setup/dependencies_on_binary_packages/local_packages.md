# 本地包依赖

配置一个外部的 jar 包依赖，你需要在 **<font color='green'>compile</font>** 配置中添加一个依赖。下面的代码添加了 `libs` 文件夹中的所有 jar 文件作为依赖。

``` Groovy
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
}

android {
    ...
}
```

> 注意：<font color='green'>dependencies</font> DSL 标签是标准 Gradle API 中的一部分，所以它不属于 <font color='green'>android</font> 标签。

**<font color='green'>compile</font>** 配置将被用于编译 main application。里面的所有依赖都会被添加到编译 classpath 中，**同时**也会被打包到最终的 APK 内。以下是其他一些添加依赖时可能用到的配置选项:

* **<font color='green'>compile</font>** 编译主 moudle
* **<font color='green'>androidTestCompile</font>** 编译主 moudle 的测试
* **<font color='green'>debugCompile</font>** debug  Build Type 的编译
* **<font color='green'>releaseCompile</font>** release Build Type 的编译

因为不可能去构建一个没有关联任何 *Build Type* 的 APK，所以 APK 默认配置了两个（或更多）的编译配置：**<font color='green'>compile</font>** 和  `<buildtype>Compile`。创建一个新的 *Build Type* 将会自动创建一个基于该名字的新配置。如果 debug 版要用一个自定义库（为了反馈实例化的崩溃信息等），但 release 版不需要，又或者 debug、release 依赖于同一个库的不同版本时，`<buildtype>Compile` 会非常有用（查看 [Gradle documentation][1] 了解更多版本冲突时的处理细节）。

[1]: https://docs.gradle.org/current/userguide/dependency_management.html#sub:version_conflicts


