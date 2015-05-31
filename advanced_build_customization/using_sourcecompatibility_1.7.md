# 使用 sourceCompatibility 1.7

使用 Android KitKat（API 19 版本的 buildTools）就可以使用 diamond operator，multi-catch，strings in switches，try with resource等等（<font color='red'>译注：</font>都是 JDK7 的一些新特性，详情请参考 JDK7 文档）。设置为 1.7 版本，需要修改你的构建文件：
``` Groovy
android {
    compileSdkVersion 19
    buildToolsVersion "19.0.0"

    defaultConfig {
        minSdkVersion 7
        targetSdkVersion 19
    }

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_7
        targetCompatibility JavaVersion.VERSION_1_7
    }
}
```

你可以将 <font color='green'>minSdkVersion</font> 的值设置为 19 之前的版本，只是你只能使用除了 try with resources 之外的其它新语言特性。如果你想要使用 try with resources 特性，你就需要把 <font color='green'>minSdkVersion</font> 也设置为 19。

sourceCompatibility 1.7 需要 Gradle 使用 1.7 或者更高版本的 JDK（Android Gradle plugin 也需要 0.6.1 或者更高的版本）。