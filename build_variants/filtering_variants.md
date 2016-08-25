# 过滤变种版本

当你添加了 dimensions 及 flavors 时，你可以移除无意义的 variants。比如你定义了一个使用 Web API 的 flavor 及一个为了更快地测试而硬编码假数据的 flavor。后者只会用于开发阶段而不会存在于发布阶段。你可以通过 **<font color='green'>variantFilter</font>** 闭包方法移除这个 variant：

``` Groovy
android {
    productFlavors {
        realData
        fakeData
    }

    variantFilter { variant ->
        def names = variant.flavors*.name

        if (names.contains("fakeData") && variant.buildType.name == "release") {
            variant.ignore = true
        }
    }
}
```

像上面那样配置后，你的项目只会存在三个 variants：

* **<font color='green'>realDataDebug</font>**
* **<font color='green'>realDataRelease</font>**
* **<font color='green'>fakeDataDebug</font>**

查看 [DSL reference][1] 了解可以通过 **<font color='green'>variant</font>** 获取的所有属性。

[1]: http://google.github.io/android-gradle-dsl/current/com.android.build.gradle.api.VariantFilter.html