# 远程包依赖

Gradle 支持从 Maven 或 Ivy 仓库中拉取依赖文件。

首先必须将仓库添加到列表中，然后必须在依赖中声明 Maven 或 Ivy 声明的文件。

``` Groovy
repositories {
    mavenCentral()
}


dependencies {
    compile 'com.google.guava:guava:11.0.2'
}

android {
    ...
}
```

---

> 注意：**<font color='green'>mavenCentral()`</font>** 是指定仓库 URL 的简单方法。Gradle 支持远程和本地仓库。

---

> 注意：Gradle 会遵循依赖关系的传递性。这意味着如果一个依赖本身依赖于其它东西，这些东西也会一并被拉取回来。

---

更多关于设置 dependencies 的信息，请参考 [Gradle用户指南][1] 和 [DSL][2] 文档。

[1]: http://gradle.org/docs/current/userguide/artifact_dependencies_tutorial.html
[2]: http://gradle.org/docs/current/dsl/org.gradle.api.artifacts.dsl.DependencyHandler.html