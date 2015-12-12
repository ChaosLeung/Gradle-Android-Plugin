# 项目结构

上面提到的构建文件中有默认的文件夹结构。Gradle 遵循约定优先于配置的概念，在尽可能的情况下提供合理的默认配置参数。最基本的项目有两个 “source sets” 组件，分别存放应用源代码及测试源代码。它们分别位于：

 * `src/main/`
 * `src/androidTest/`

里面每个存在的文件夹对应相应的源组件。对于 Java plugin 和 Android plugin 来说，它们的 Java 源代码和资源文件路径如下：

* `java/`
* `resources/`

但对于 Android plugin 来说，它还拥有以下特有的文件和文件夹结构：

* `AndroidManifest.xml` 
* `res/`
* `assets/`
* `aidl/`
* `rs/`
* `jni/`
* `jniLibs/`

这就意味着在 Android plugin 下 `*.java` 文件的 source set 路径是 `src/main/java`，而 manifest 则是 `src/main/AndroidManifest.xml`

> 注意：`src/androidTest/AndroidManifest.xml` 会被自动创建，所以一般情况下不需要手动创建。