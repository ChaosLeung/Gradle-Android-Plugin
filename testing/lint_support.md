# Lint 支持

你可以为特定 variant 运行 lint，例如 **<font color='green'>./gradlew lintRelease</font>**，或为所有版本运行（**<font color='green'>./gradlew lint</font>**），这种情况下会生成一份包含特定版本存在的问题的详细报告。你可以像下面的代码片段那样通过配置 lintOptions 节点来配置 lint。一般只能配置小部分选项，查看 [DSL reference](http://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.LintOptions.html#com.android.build.gradle.internal.dsl.LintOptions) 了解所有可修改的选项。

``` Groovy
android {
    lintOptions {
        // turn off checking the given issue id's
        disable 'TypographyFractions','TypographyQuotes'

        // turn on the given issue id's
        enable 'RtlHardcoded','RtlCompat', 'RtlEnabled'

        // check *only* the given issue id's
        check 'NewApi', 'InlinedApi'
    }
}
```