# 产品定制

Product flavor 可定义应用的不同定制版本，一个项目可以同时定义多个不同的 flavor 来改变应用的输出。

不同定制版本之间的差异非常小的情况，可以考虑使用 Product flavor。虽然项目最终会生成多个定制版本，但是它们本质上都是同一个应用。这种做法可能是比使用 Library 项目更好的实现方式。

Product flavor 需要在 **<font color='green'>productFlavors</font>** 这个 DSL 容器中声明：

``` Groovy
android {
    ....

    productFlavors {
        flavor1 {
            ...
        }

        flavor2 {
            ...
        }
    }
}
```

这里创建了两个flavor，名为 **<font color='green'>flavor1</font>** 和 **<font color='green'>flavor2</font>**。

> 注意：flavor 的命名不能与已存在的 *Build Type* 或者与 **<font color='green'>androidTest</font>**、**<font color='green'>test</font>** *sourceSet* 有冲突。