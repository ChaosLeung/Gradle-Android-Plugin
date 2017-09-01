# 普通项目和 Library 项目的区别

Library 项目会输出 [*.aar* 包][1]（Android 应用模块依赖项的 Android 归档文件）。包含编译文件（以 jar 包或者 .so 文件形式）和资源文件（manifest, res, assets）。Library 项目同样也可以借助普通项目生成测试 apk 进行测试。标识 Task 同样适用于 Library 项目（**<font color='green'>assembleDebug</font>**，**<font color='green'>assembleRelease</font>**），因此在命令行构建的方式都是一样的。至于其他方面，Library 项目与 Application 项目相同。它们都拥有 `build types` 和 `product flavors`（后面会提到），也可以生成多个不同版本的 `aar`。**注意**大部分 *Build Type* 的配置不适用于 Library 项目。但可以根据 Library 项目是被普通项目使用还是被用来测试来自定义 *sourceSet* 中的内容。

[1]: ../../appendix/aar_format.md