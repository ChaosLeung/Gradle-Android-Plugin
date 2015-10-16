# 解决 main APK 与 test APK 之间的冲突

> 注意： 该章节的内容均为直译，由于个人测试的结果跟文章说的内容存在差异，所以并不确定字里行间的真正意思。如果存疑，请结合[官网原文][0]阅读。

[0]:http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Resolving-conflicts-between-main-and-test-APK

当 instrumentation 测试用例运行时，main APK 与 test APK 共享相同的 classpath。如果 main APK 与 test APK 使用相同的库（例：Guava）但版本不同的时候，Gradle 将会构建失败。如果 Gradle 没有对这部分问题进行处理（<font color='red'>译注：</font>估计这里是指旧版本 Gradle 没处理这个问题，但我用 0.10.+ 的 android plugin、1.11 的 gradle 也没出现构建失败），你的应用在测试和正常运行过程中会出现不同的行为（包括崩溃的表现也可能不一样）。

为了构建成功，只需确定这两个 apk 使用相同版本的库。如果是由于间接依赖（没有在你的 build.gradle 提及的库）而导致构建错误，只需添加对应的新版本库依赖到配置中（"compile" 或 "androidTestCompile"），你也可以使用 [Gradle's resolution strategy mechanism][1] 来解决错误。

> <font color='red'>译注：</font>Gradle's resolution strategy mechanism，是 Gradle 用于定义解析依赖策略的 API，可用于强制指定依赖库的版本、库的替代策略、冲突解决、库缓存本地的时间等

[1]: https://docs.gradle.org/current/dsl/org.gradle.api.artifacts.ResolutionStrategy.html

你可以通过运行 **<font color='green'>./gradlew :app:dependencies</font>** 命令查阅依赖树