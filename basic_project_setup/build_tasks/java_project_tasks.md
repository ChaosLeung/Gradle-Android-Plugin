# Java 项目的 Task

这里有两个由 Java plugin 创建的十分重要的 task，它们依赖于前面所述的标志性 task：

* **<font color='green'>assemble</font>**
  * **<font color='green'>jar</font>** 该 task 创建所有输出
* **<font color='green'>check</font>**
  * **<font color='green'>test</font>** 该 task 执行所有测试

**<font color='green'>jar</font>** task 本身直接或者间接依赖于其他 task:
**<font color='green'>classes</font>** task 将会被调用于编译 Java 代码。**<font color='green'>testClasses</font>** task 用于编译测试，但是很少被调用，因为 **<font color='green'>test</font>** task 依赖于它（以及 **<font color='green'>classes</font>** task）。

通常情况下，你可能只需要调用 **<font color='green'>assemble</font>** 和 **<font color='green'>check</font>**，而不需要其他 task。你可以在 Gradle 文档中查看 [Java plugin][1] 的全部 task 已经它们之间的依赖。

[1]: http://gradle.org/docs/current/userguide/java_plugin.html