# 普通项目和 Library 项目的区别

Library 项目 main 输出一个 *.aar*  包，包含编译文件（类似 jar 包或者 .so 文件）和资源文件（manifest，res，assets）。

Library 项目同样也可以独立于应用程序生成一个测试用的 apk 来测试。

标识 Task 同样适用于 Library 项目（**<font color='green'>assembleDebug</font>**，**<font color='green'>assembleRelease</font>**），因此在命令行构建项目没有什么不同。

至于其他的，Library 项目跟应用工程一样，它们都拥有 `build type` 和 `product flavor`，也可以生成多个不同版本的 `aar`。   
大部分 *Build Type* 的配置不适用于 Library 项目。但可以根据 Library 项目 `是否被其它项目使用`，`是否用来测试` 来作为使用自定义 *sourceSet* 的条件，从而动态使用 Library 项目的资源。
