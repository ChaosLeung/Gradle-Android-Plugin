# 测试

测试 multi-flavors 项目非常类似于测试简单的项目。

**<font color='green'>androidTest</font>** 的 *sourceSet* 用于定义所有 flavor 共用的测试，但是每一个 flavor 也可以有它特有的测试。

正如前面提到的，每一个 flavor 都会创建自己的测试 sourceSet：

* **<font color='green'>android.sourceSets.androidTestFlavor1</font>**
 位于 `src/androidTestFlavor1/`
* **<font color='green'>android.sourceSets.androidTestFlavor2</font>**
 位于 `src/androidTestFlavor2/`

同样的，它们也可以拥有自己的依赖关系：

``` Groovy
dependencies {
    androidTestFlavor1Compile "..."
}
```

这些测试可以通过主要的标志性 **<font color='green'>deviceCheck</font>** task 或者主要的 **<font color='green'>androidTest</font>** task（当 flavor 被使用的时候这个 task 相当于一个标志性 task）来执行。

每个 flavor 也拥有自己的 task 来执行测试：`androidTest<VariantName>`。例如：

* **<font color='green'>androidTestFlavor1Debug</font>**
* **<font color='green'>androidTestFlavor2Debug</font>**

同样的，每个 variant 版本也会创建对应的测试 APK 构建 task 和 安装或卸载 task：

* **<font color='green'>installFlavor1Debug</font>**
* **<font color='green'>assembleFlavor1Test</font>**
* **<font color='green'>installFlavor1Test</font>**
* **<font color='green'>uninstallFlavor1Debug</font>**
* ...

最终的 HTML 报告根据每个 flavor 的报告汇总而成。  
下面是测试结果和报告文件的路径，每组第一个是每个 flavor 版本的结果，第二个是汇总结果：

* `build/androidTest-results/flavors/<FlavorName>`
* `build/androidTest-results/all/`
* `build/reports/androidTests/flavors<FlavorName>`
* `build/reports/androidTests/all/`

改变 report 或 results 的输出文件夹都只会改变对应的根目录，构建时仍会创建每个 flavor 的文件夹，并且仍会汇总测试结果以及报告文件。