# Library 项目发布

一般情况下一个库只会发布它的 *release* variant（变种）版本。这个版本将会被所有引用它的项目使用，而不管它们本身自己构建了什么版本。这是由于 Gradle 的限制，我们正在努力解决这个问题，所以这只是临时的限制。

你可以控制哪一个 Variant 版本作为发行版：

``` Groovy
android {
    defaultPublishConfig "debug"
}
```

注意这里的发布配置名称引用的是完整的 variant 版本名称。*Relesae*，*debug* 只适用于项目中没有其它 flavor（特性）时使用。如果想要用其它使用了 flavor 的 variant 版本取代默认的发布版本，你可以：

``` Groovy
android {
    defaultPublishConfig "flavor1Debug"
}
```

将 Library 项目的所有 variant 版本都发布也是可能的。我们计划在一般的 `项目依赖项目`（类似于前面所述）情况下允许这种做法，但是由于 Gradle 的限制（我们也在努力修复这个问题）现在还不太可能。  
默认情况下没有开启发布所有 variant 版本功能，可以通过以下代码启用：

``` Groovy
android {
    publishNonDefault true
}
```

发布多个 variant 版本意味着发布多个 aar 文件而不是一个 aar 文件包含所有 variant 版本。每个 aar 包都包含一个 variant 版本。  
发布一个 variant 版本意味着构建一个可用的 aar 文件作为 Gradle 项目的输出文件。无论是发布到 maven 仓库，还是其它项目需要创建该 Library 项目的依赖都可以使用到这个 aar。

Gradle 有`默认文件`的概念。当添加以下配置后就会自动使用：

``` Groovy
compile project(':libraries:lib2')
```

创建其它发布文件的依赖，你需要指定具体使用哪一个：

``` Groovy
dependencies {
    flavor1Compile project(path: ':lib1', configuration: 'flavor1Release')
    flavor2Compile project(path: ':lib1', configuration: 'flavor2Release')
}
```

---

> 重要：注意已发布的 configuration 是一个完整的 variant 版本，其中包括了 build type，并且需要像上面一样被引用。

---

> 重要：当发布配置非默认时，Maven 发布插件将会发布其它 variant 版本作为扩展包（按分类器分类）。这里是指不能真正的兼容发布到 Maven 仓库。你应该另外发布一个单一的 variant 版本到仓库中，或者允许发布所有配置以支持跨项目依赖。

---