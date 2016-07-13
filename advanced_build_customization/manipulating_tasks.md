# 操作 task

一般的 Java 项目中有一组 task 用于协同处理并最终生成一个输出。  
**<font color='green'>classes</font>** task 用于编译 Java 源代码。  
可以在 *build.gradle* 文件中使用 **<font color='green'>classes</font>** 访问 **<font color='green'>classes</font>** task 。**<font color='green'>classes</font>** 是 **<font color='green'>project.tasks.classes</font>** 的缩写。

相比之下在 Android 项目中这就有点复杂。因为 Android 项目中会有大量相同的 task，并且它们的名字基于 *Build Types* 和 *Product Flavor* 生成。

为了解决这个问题，**<font color='green'>android</font>** 对象有三个属性：

* **<font color='green'>applicationVariants</font>**（只适用于 app plugin）
* **<font color='green'>libraryVariants</font>**（只适用于 library plugin）
* **<font color='green'>testVariants</font>**（app、library plugin 均适用）

这三个属性会分别返回一个 `ApplicationVariant`、`LibraryVariant` 和 `TestVariant` 对象的 [DomainObjectCollection][1]。

注意，使用这三个 collection 中的其中一个都会触发生成所有对应的 task。这意味着使用 collection 之后不需要重新配置。

`DomainObjectCollection` 可以直接访问所有对象，或者通过过滤器进行筛选。

``` Groovy
android.applicationVariants.each { variant ->
    ....
}
```

这三个 variant 类都拥有下面的属性：

属性名	       	|属性类型	    |说明
:-------------  	|:-------------| :-----
name	        |String	|Variant 的名字，唯一
description		|String	|Variant 的描述说明
dirName	    	|String|Variant 的子文件夹名，唯一。可能有不止一个子文件夹，例如 “debug/flavor1”
baseName	    |String	|Variant 输出的基础名字，必须唯一
outputFile	    |File	|Variant 的输出，该属性可读可写
processManifest	|ProcessManifest	|处理 Manifest 的 task
aidlCompile		|AidlCompile	|编译 AIDL 文件的 task
renderscriptCompile	|RenderscriptCompile    	|编译 Renderscript 文件的 task
mergeResources	|MergeResources	|合并资源文件的 task
mergeAssets		|MergeAssets	|合并 assets 的 task
processResources|ProcessAndroidResources	|处理并编译资源文件的 task
generateBuildConfig	|GenerateBuildConfig	|生成 BuildConfig 类的 task
javaCompile		|JavaCompile	|编译 Java 源代码的 task
processJavaResources|Copy	|处理 Java 资源的 task
assemble		|DefaultTask	|Variant 的标志性 assemble task

`ApplicationVariant` 类还有以下附加属性：

属性名			|属性类型	|说明
:-------------  	|:-------------| :-----
buildType		|BuildType	|Variant 的 BuildType
productFlavors	|List&lt;ProductFlavor>	|Variant 的 ProductFlavor，一般不为空但允许为空
mergedFlavor	|ProductFlavor	|android.defaultConfig 和 variant.productFlavors 的组合
signingConfig	|SigningConfig	|Variant 使用的 SigningConfig 对象
isSigningReady	|boolean	|如果是 true 则表明该 Variant 已经具备了所有需要签名的信息
testVariant		|BuildVariant	|将会测试该 Variant 的 TestVariant
dex				|Dex	|将代码打包成 dex 的 task。如果该 Variant 是 Library，该值可为空
packageApplication	|PackageApplication	|打包最终 APK 的 task。如果该 Variant 是 Library，该值可为空
zipAlign		|ZipAlign	|对 APK 进行 zipalign 的 task。如果该 Variant 是 Library 或者 APK 不能被签名时，该值可为空
install		|DefaultTask	|负责安装的 task，可为空
uninstall	|DefaultTask	|负责卸载的 task

`LibraryVariant` 类还有以下附加属性：

属性名			|属性类型	|说明
:-------------  	|:-------------| :-----
buildType		|BuildType	|Variant 的 BuildType
mergedFlavor	|ProductFlavor	|只有 android.defaultConfig
testVariant		|BuildVariant	|用于测试 Variant
packageLibrary	|Zip	|用于打包 Library 项目的 AAR 文件。如果是 Library 项目，该值不能为空

`TestVariant` 类还有以下属性：

属性名			|属性类型	|说明
:-------------  	|:-------------| :-----
buildType	|BuildType	|Variant 的 Build Type
productFlavors	|List&lt;ProductFlavor>	|Variant 的 ProductFlavor。一般不为空但允许为空
mergedFlavor	|ProductFlavor	|android.defaultConfig 和 variant.productFlavors 的组合
signingConfig	|SigningConfig	|Variant 使用的 SigningConfig 对象
isSigningReady	|boolean	|如果是 true 则表明该 Variant 已经具备了所有需要签名的信息
testedVariant	|BaseVariant	|TestVariant 测试的 BaseVariant
dex	|Dex	|将代码打包成 dex 的 task。如果该 Variant 是 Library，该值可为空
packageApplication	|PackageApplication	|打包最终 APK 的 task。如果该 Variant 是 Library，该值可为空
zipAlign	|ZipAlign	|对 APK 进行 zipalign 的 task。如果该 Variant 是 Library 或者 APK 不能被签名时，该值可为空
install	|DefaultTask	|负责安装的 task，可为空
uninstall	|DefaultTask	|负责卸载的 task
connectedAndroidTest	|DefaultTask	|在连接设备上执行 Android 测试的 task
providerAndroidTest	|DefaultTask	|使用扩展 API 执行 Android 测试的 task

Android task 特有类型的 API：

* `ProcessManifest`
    * `File manifestOutputFile`
* `AidlCompile`
    * `File sourceOutputDir`
* `RenderscriptCompile`
    * `File sourceOutputDir`
    * `File resOutputDir`
* `MergeResources`
    * `File outputDir`
* `MergeAssets`
    * `File outputDir`
* `ProcessAndroidResources`
    * `File manifestFile`
    * `File resDir`
    * `File assetsDir`
    * `File sourceOutputDir`
    * `File textSymbolOutputDir`
    * `File packageOutputFile`
    * `File proguardOutputFile`
* `GenerateBuildConfig`
    * `File sourceOutputDir`
* `Dex`
    * `File outputFolder`
* `PackageApplication`
    * `File resourceFile`
    * `File dexFile`
    * `File javaResourceDir`
    * `File jniDir`
    * `File outputFile`
        * 直接在 Variant 对象中使用 “outputFile” 可以改变最终的输出文件夹。
* `ZipAlign`
    * `File inputFile`
    * `File outputFile`
        * 直接在 Variant 对象中使用 “outputFile” 可以改变最终的输出文件夹。

每个 task 类型的 API 都受 Gradle 的工作方式和 Android plugin 的配置方式限制。  
首先，Gradle 中存在的 task 只能配置输入输出的路径以及部分可能使用的可选标识。因此，这些 task 只能定义一些输入或者输出。

其次，这里面大多数 task 的输入都不是单一的，一般都混合了 *sourceSet*、*Build Type* 和 *Product Flavor* 中的值。所以为了保持构建文件的简洁和可读性，目标自然是让开发者通过 DSL 修改这些对象来影响构建的过程，而不是深入修改输入和 task 的选项。

另外需要注意，上面的 task 中除了 ZipAlign，其它都要求设置私有数据进行工作。这意味着不能手动创建这些类型的 task 实例。

这些 API 也可能会被修改。一般来说，目前的 API 是围绕着 task 的输出和输入（如果可能）来添加额外的处理（必要时）。欢迎反馈意见，特别是那些没有考虑过的需求。

对于 Gradle 的 task（DefaultTask，JavaCompile，Copy，Zip），请参考 Gradle 文档。

[1]: http://www.gradle.org/docs/current/javadoc/org/gradle/api/DomainObjectCollection.html