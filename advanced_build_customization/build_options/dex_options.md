# dex 选项

``` Groovy
android {
    dexOptions {
        incremental false
        preDexLibraries = false
        jumboMode = false
        javaMaxHeapSize "2048M"
    }
}
```

这将会影响到所有使用 dex 的 task。