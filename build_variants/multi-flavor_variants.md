# 多定制的变种版本

某些情况下，应用可能需要基于多个标准来创建多个版本。  
例如，Google Play 中的 multi-apk 支持 4 种过滤器。根据每个过滤器来创建不同的 APK 需要使用 *Product Flavor* 分组。

假如有个游戏有免费版和付费版，并且需要在 multi-apk 支持中使用 ABI 过滤器。该游戏应用需要 3 个 ABI 和两个特定版本，因此就需要生成 6 个 APK（忽略不同 *Build Types* 生成的 variant 版本）。  
然而，3 个 ABI 付费版的源代码都是相同的，因此创建 6 个 flavor 来实现并不是一个好办法。  
作为代替，可以使用两个 flavor 分组，并且让它自动构建所有可能的 variant 组合。

对应的功能实现需要使用 Flavor Dimensions（<font color='red'>译注：</font> `Flavor Dimensions` 对应旧版中的 `Flavor Groups`），并将 flavor 分配到一个指定的 dimension 中。

``` Grovvy
android {
    ...


    flavorDimensions "abi", "version"


    productFlavors {
        freeapp {
            dimension "version"
            ...
        }

        paidapp {
            dimension "version"
            ...
        }


        arm {
            dimension "abi"
            ...
        }

        mips {
            dimension "abi"
            ...
        }

        x86 {
            dimension "abi"
            ...
        }
    }
}
```

**<font color='green'>andorid.flavorDimensions</font>** 数组按照先后排序定义了可能用到的分组。（示例中）每个 *Product Flavor* 都被分配到一个分组中。

示例中将 *Product Flavor* 分为两组，为别为 abi [x86,arm,mips] 和 version [freeapp,paidapp]，再加上默认的 *Build Type* [debug,release]，最后会生成以下的 Build Variant：

* `x86-freeapp-debug`
* `x86-freeapp-release`
* `arm-freeapp-debug`
* `arm-freeapp-release`
* `mips-freeapp-debug`
* `mips-freeapp-release`
* `x86-paidapp-debug`
* `x86-paidapp-release`
* `arm-paidapp-debug`
* `arm-paidapp-release`
* `mips-paidapp-debug`
* `mips-paidapp-release`

**<font color='green'>andorid.flavorDimensions</font>** 中元素的顺序非常重要（variant 命名和优先级等）。

每个 variant 版本的配置由几个 *Product Flavor* 对象决定：

* **<font color='green'>android.defaultConfig</font>**
* 一个来自 abi 组中的对象
* 一个来自 version 组中的对象

flavorDimensions 中的顺序决定了 flavor 的优先级，这对于资源来说非常重要，因为 flavor 中的值会替换定义在低优先级的 flavor 中的值。  
flavor dimension 使用最高的优先级定义，因此前面例子中的优先级为：

    abi > version > defaultConfig

Multi-flavors 项目同样拥有额外的 sourceSet，类似于 variant 的 sourceSet，只是少了 Build Type：

* **<font color='green'>android.sourceSets.x86Freeapp</font>**
位于 `src/x86Freeapp/`
* **<font color='green'>android.sourceSets.armPaidapp</font>**
位于 `src/armPaidapp/`
* 等等...

这允许在 flavor-combination（组合 flavor）的层次上进行定制。它们拥有比最基本的 flavor 的 sourceSet 更高的优先级，但是优先级低于 Build Type 的 sourceSet。