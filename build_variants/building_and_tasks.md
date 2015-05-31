# 构建和任务

我们前面提到每一个 *Build Type* 会创建自己的 `assemble<name>` task，但是 *Build Variant* 是 *Build Type* 和 *Product Flavor* 的组合。

当使用 *Product Flavor* 的时候，将会创建更多的 assemble-type task。分别是：

1. `assemble<Variant Name>`
允许直接构建一个 variant 版本，例如 **<font color='green'>assembleFlavor1Debug</font>**。
2. `assemble<Build Type Name>`
允许构建指定 Build Type 的所有 APK，例如 **<font color='green'>assembleDebug</font>** 将会构建 `Flavor1Debug` 和 `Flavor2Debug` 两个 variant 版本。
3. `assemble<Product Flavor Name>`
允许构建指定 flavor 的所有 APK，例如 **<font color='green'>assembleFlavor1</font>** 将会构建 `Flavor1Debug` 和 `Flavor1Release` 两个 variant 版本。

另外 **<font color='green'>assemble</font>** task 会构建所有的 variant 版本。