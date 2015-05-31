# 通用任务

添加一个插件到构建文件中将会自动创建一系列构建任务（build tasks）去执行（注：Gradle 属于任务驱动型构建工具，构建过程基于 Task）。Java 插件和 Android 插件都会创建以下 Task:

* **<font color='green'>assemble</font>** 
组合项目所有输出任务
* **<font color='green'>check</font>** 
执行所有检查任务
* **<font color='green'>build</font>** 
执行 **<font color='green'>assemble</font>** 和 **<font color='green'>check</font>** 两个 task 的所有工作
* **<font color='green'>clean</font>**
会清空项目的输出

实际上 **<font color='green'>assemble</font>**，**<font color='green'>check</font>** 和 **<font color='green'>build</font>** 这三个 task 不做任何事情。它们只是一个 Task 标志，用来告诉 plugin 添加实际需要执行的 task 去完成这些工作。

这就允许你去调用相同的 task，而不需要考虑当前是什么类型的项目，或者当前项目添加了什么 plugin。例如，添加了 *findbugs* plugin 将会创建一个新的 task 并且让 **<font color='green'>check</font>** task 依赖于这个新的 task。当 **<font color='green'>check</font>** task 被调用的时候，这个新的 task 将会先被调用。

在命令行环境中，你可以执行以下命令来获取更多高级别的 task：

``` Groovy
gradle tasks
```

查看所有 task 列表和它们之间的依赖关系可以执行以下命令：

``` Groovy
gradle tasks --all
```

---

> 注意：Gradle 会自动监视一个 task 声明的所有输入和输出。 两次执行 **<font color='green'>build</font>** task 并且期间项目没有任何改动，Gradle 将会使用`UP-TO-DATE` 通知所有 task。这意味着第二次 build 执行的时候不会请求任何 task 执行。这允许 task 之间互相依赖，而不会导致不需要的构建请求被执行。

---
