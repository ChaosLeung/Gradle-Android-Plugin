# 普通项目和 Library 项目的区别

Library 项目输出一个 [*.aar* 包][1]（标准的 Android archive）。包含编译文件（类似 jar 包或者 .so 文件）和资源文件（manifest，res，assets）。Library 项目同样也可以独立于应用程序生成一个测试用的 apk 来测试。标识 Task 同样适用于 Library 项目（**<font color='green'>assembleDebug</font>**，**<font color='green'>assembleRelease</font>**），因此在命令行构建项目与普通项目相差无几。至于其他方面，Library 项目与 Application 项目相同。它们都拥有 `build types` 和 `product flavors`（后面会提到），也可以生成多个不同版本的 `aar`。注意大部分 *Build Type* 的配置不适用于 Library 项目。但可以根据 Library 项目被哪些项目使用或是否是用来测试来自定义 *sourceSet* 中的内容。

[1]: http://tools.android.com/tech-docs/new-build-system/aar-format