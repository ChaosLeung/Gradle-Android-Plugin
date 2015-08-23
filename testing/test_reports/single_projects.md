# 独立项目

一个项目将会自动生成测试运行。默认位置为：

`build/reports/androidTests`

类似于 JUnit 的报告所在位置 `build/reports/tests`，其它的报告通常位于 `build/reports/&lt;plugin>/`

这个路径也可以通过以下方式自定义：

``` Groovy
android {
    ...

    testOptions {
        reportDir = "$project.buildDir/foo/report"
    }
}
```

报告将会合并运行在不同设备上的测试结果。