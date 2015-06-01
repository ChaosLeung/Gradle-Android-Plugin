# Java 项目的 Task

Java plugin 主要创建了两个 task，依赖于主要的 task（一个标识性的 task）：

* **<font color='green'>assemble</font>**
  * **<font color='green'>jar</font>** 该 task 创建所有输出
* **<font color='green'>check</font>**
  * **<font color='green'>test</font>** 该 task 执行所有测试

**<font color='green'>jar</font>** task 本身直接或者间接依赖于其他 task:
**<font color='green'>classes</font>** task 将会被调用于编译 Java 代码。**<font color='green'>testClasses</font>** task 用于编译测试，但是很少被调用，因为 **<font color='green'>test</font>** task 依赖于它（类似于 **<font color='green'>classes</font>** task）。

通常情况下，你可能只需要调用 **<font color='green'>assemble</font>** 和 **<font color='green'>check</font>**，而不需要其他 task。

你可以在 Gradle 文档中查看 [Java plugin](http://gradle.org/docs/current/userguide/java_plugin.html) 的全部 task。


