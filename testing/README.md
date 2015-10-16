# 测试

测试项目已经被集成到应用项目中，没有必要再专门建立一个测试项目。

Android Studio 1.1 添加了单元测试支持（实验性功能），详细请看 [Unit testing support][1]。本章的其余部分描述的是 “instrumentation tests”，利用 Instrumentation 测试框架可以构建一个独立的测试 APK 并运行在真实设备（或模拟器）中以测试。

[1]: http://tools.android.com/tech-docs/unit-testing-support