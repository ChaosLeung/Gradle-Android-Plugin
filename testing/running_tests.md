#  运行测试

正如前面提到的，**<font color='green'>connectedCheck</font>** 需要一个已连接设备。这个过程依赖于 **<font color='green'>connectedDebugAndroidTest</font>** task，因此 **<font color='green'>connectedDebugAndroidTest</font>** task 也会运行。该 task 会执行以下内容：

* 确认应用和测试应用已被构建（依赖于 **<font color='green'>assembleDebug</font>** 和 **<font color='green'>assembleDebugAndroidTest</font>**）
* 安装这两个应用
* 运行测试
* 卸载这两个应用

如果有多个连接设备，测试会并行在所有连接设备上。如果其中一个测试失败，不管在哪个设备都算测试失败。