# 产品定制的配置

每个 flavor 都是通过闭包来配置的：

``` Groovy
android {
    ...

    defaultConfig {
        minSdkVersion 8
        versionCode 10
    }

    productFlavors {
        flavor1 {
            packageName "com.example.flavor1"
            versionCode 20
        }

        flavor2 {
            packageName "com.example.flavor2"
            minSdkVersion 14
        }
    }
}
```

注意 *ProductFlavor* 类型的 **<font color='green'>android.productFlavors.*</font>** 对象与 **<font color='green'>android.defaultConfig</font>** 对象的类型是相同的。就是说着它们之间属性共享。

**<font color='green'>defaultConfig</font>** 为所有的 flavor 提供基本的配置，每个 flavor 都可以重写这些配置的值。在前面的例子中，最终的配置结果将会是：

* **<font color='green'>flavor1</font>**
    * **<font color='green'>applicationId</font>**: com.example.flavor1
    * **<font color='green'>minSdkVersion</font>**: 8
    * **<font color='green'>versionCode</font>**: 20
* **<font color='green'>flavor2</font>**
    * **<font color='green'>applicationId</font>**: com.example.flavor2
    * **<font color='green'>minSdkVersion</font>**: 14
    * **<font color='green'>versionCode</font>**: 10

通常情况下，*Build Type* 的配置会覆盖其它的配置。例如，*Build Type* 的 **<font color='green'>applicationIdSuffix</font>** 会被追加到 *Product Flavor* 的 **<font color='green'>applicationId</font>** 上面。但有部分属性可以同时在 *Build Type* 和 *Product Flavor* 中设置。在这种情况下，按照个别为主的原则决定。例如，通过设置 **<font color='green'>android.buildTypes.release.signingConfig</font>** 来为所有的 release 包共用相同的 *SigningConfig*。也可以通过设置 **<font color='green'>android.productFlavors.*.signingConfig</font>** 来为每个 release 包指定它们自己的 *SigningConfig*。