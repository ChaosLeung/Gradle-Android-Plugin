# Android Tasks

Android plugin 使用相同的约定以兼容其他插件，并且附加了标志性的 task，包括:

* **<font color='green'>assemble</font>** 
组合项目所有输出
* **<font color='green'>check</font>** 
执行所有检查
* **<font color='green'>connectedCheck</font>** 
在一个连接的设备或者模拟器上执行检查，它们可以在所有连接的设备上并行执行检查
* **<font color='green'>deviceCheck</font>** 
通过 APIs 连接远程设备来执行检查，主要用于 CI（Continuos integration ，持续集成）服务上。
* **<font color='green'>build</font>** 
执行 **<font color='green'>assemble</font>** 和 **<font color='green'>check</font>** 的所有工作
* **<font color='green'>clean</font>** 
清空项目的输出

这些新的标志性 task 是必须的，以保证能够在没有设备连接的情况下执行定期检查。 注意 **<font color='green'>build</font>** task 不依赖于 **<font color='green'>deviceCheck</font>** 或者 **<font color='green'>connectedCheck</font>**。

一个 Android 项目至少拥有两个输出：debug APK 和 release APK。每个输出都有各自的标志性 task 以便单独构建它们。

* **<font color='green'>assemble</font>**
  * **<font color='green'>assembleDebug</font>**
  * **<font color='green'>assembleRelease</font>**

它们都依赖于其它一些 tasks 以完成构建一个APK所需的多个步骤。其中 **<font color='green'>assemble</font>** task 依赖于上述两个 task，所以执行 **<font color='green'>assemble</font>** 将会同时构建出两个 APK。

> 提示: Gradle 在命令行上支持驼峰命名法的 task 简称，例如，执行
> 
> ``` gradle
> gralde aR
> ```  
> 
> 等同与输入  
> 
> ``` gradle
> gradle assembleRelease
> ```  
> 
> 只要没有其它命令匹配 `aR` 
>  
> <font color='red'>译者注：</font>assR 同样能运行 assembleRelease task，即简称不一定要是首字母缩写 \_(:зゝ∠)\_

check task 也有拥有依赖:

* **<font color='green'>check</font>**
  * **<font color='green'>lint</font>**
* **<font color='green'>connectedCheck</font>**
  * **<font color='green'>connectedAndroidTest</font>**
* **<font color='green'>deviceCheck</font>**
  * 进行测试时才会触发

最后，只要可被安装（需要签名），插件会为所有的构建类型（**<font color='green'>debug, release, test</font>**）创建 install 及 uninstall 相关的 task。例：

* **<font color='green'>installDebug</font>**
* **<font color='green'>installRelease</font>**
* **<font color='green'>uninstallAll</font>**
  * **<font color='green'>uninstallDebug</font>**
  * **<font color='green'>uninstallRelease</font>**
  * **<font color='green'>uninstallDebugAndroidTest</font>**