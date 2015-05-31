#  运行测试

正如前面提到的，标志性 task **<font color='green'>connectedCheck</font>** 需要一个连接的设备来启动。  
这个过程依赖于 **<font color='green'>androidTest</font>** task，因此 **<font color='green'>androidTest</font>** task 将会运行。这个 task 将会执行下面内容：

* 确认应用和测试应用都被构建（依赖于 **<font color='green'>assembleDebug</font>** 和 **<font color='green'>assembleTest</font>**）
* 安装这两个应用
* 运行这些测试
* 卸载这两个应用

如果有多个连接设备，那么测试会并行在所有连接设备上。如果其中一个测试失败，不管在哪个设备都算测试失败。

所有测试结果都被保存为 XML 文档，路径为：

*`build/androidTest-results`*

（这类似于 JUnit 的运行结果保存在 build/test-results)

路径同样可以自定义配置：

``` Groovy
android {
    ...

    testOptions {
        resultsDir = "$project.buildDir/foo/results"
    }
}
```

**<font color='green'>android.testOptions.resultsDir</font>** 的值由 **<font color='green'>Project.file(String)</font>** 获得。