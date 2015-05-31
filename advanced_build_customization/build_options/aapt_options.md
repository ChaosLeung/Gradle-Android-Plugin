# aapt 选项

``` Groovy
android {
    aaptOptions {
        noCompress 'foo', 'bar'
        ignoreAssetsPattern "!.svn:!.git:!.ds_store:!*.scc:.*:<dir>_*:!CVS:!thumbs.db:!picasa.ini:!*~"
    }
}
```

这将会影响所有使用 aapt 的 task。