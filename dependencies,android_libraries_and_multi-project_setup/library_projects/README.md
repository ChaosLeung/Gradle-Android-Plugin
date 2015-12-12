# Library 项目

在上面的多项目配置中，**<font color='green'>:libraries:lib1</font>** 和 **<font color='green'>:libraries:lib2</font>** 可以是 Java 项目，并且 **<font color='green'>:app</font>** 这个 Android 项目将会使用它们的 *jar* 包输出。然而，如果你想要共享代码来访问 Android APIs 或者使用 Android 的资源，那么这些 Library 项目就不能是普通的 Java 项目，而应该是 Android Library 项目。