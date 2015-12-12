# 测试报告

当运行单元测试的时候，Gradle 会输出一份 HTML 格式的报告以方便查看结果。Android plugin 则将所有连接设备的测试报告都合并到一个 HTML 格式的报告文件中。所有测试结果都以 XML 文件形式保存到 `build/reports/androidTests/` 中（类似于 JUnit 的运行结果保存在 build/reports/tests 中)。可以自定义路径：

``` Groovy
android {
    ...

    testOptions {
        resultsDir = "${project.buildDir}/foo/results"
    }
}
```

**<font color='green'>android.testOptions.resultsDir</font>** 的值由 **<font color='green'>Project.file(String)</font>** 计算获得。