# 设置 Java 的版本

你可以使用 **<font color='green'>compileOptions</font>** 块选择编译器使用的版本。默认由 **<font color='green'>compileSdkVersion</font>** 的值来决定。

``` Groovy
android {
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_6
        targetCompatibility JavaVersion.VERSION_1_6
    }
}
```