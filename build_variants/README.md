# 构建 Variants（变种）版本

新构建系统的一个目标就是允许为同一个应用创建不同的版本。

这里有两个主要的使用情景：

1. 同一个应用的不同版本。例如，免费的版本和收费的专业版本。
2. 同一个应用需要打包成不同的 apk 以发布 Google Play Store，查看 [Multiple APK Support][1] 了解详情。
3. 综合 1 和 2 两种情景。

该目标就是要让在同一个项目里生成不同的 APK 成为可能，以取代以前需要使用一个库项目和两个或以上的应用项目分别生成不同 APK 的做法。

[1]: http://developer.android.com/google/play/publishing/multiple-apks.html