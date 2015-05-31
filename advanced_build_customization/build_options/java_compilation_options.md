# Java 编译选项

``` Groovy
android {
    compileOptions {
        sourceCompatibility = "1.6"
        targetCompatibility = "1.6"
    }
}
```

默认值是 “1.6” 。该设置将会影响所有需要编译 Java 源代码的 task。