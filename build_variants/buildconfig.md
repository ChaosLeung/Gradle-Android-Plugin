# BuildConfig

在编译时，Android Studio 会生成一个名为 **<font color='green'>BuildConfig</font>** 的类，它包含了一些编译特定 variant 时使用到的常量指。你可以通过检查这些常量的值来改变不同的 variant 的行为，例如：

``` Java
private void javaCode() {
    if (BuildConfig.FLAVOR.equals("paidapp")) {
        doIt();
    else {
        showOnlyInPaidAppDialog();
    }
}
```

BuildConfig 包含的值如下：

* **<font color='green'>boolean DEBUG</font>** —— 当前构建是否开启了 debuggable
* **<font color='green'>int VERSION_CODE</font>**
* **<font color='green'>String VERSION_NAME</font>**
* **<font color='green'>String APPLICATION_ID</font>**
* **<font color='green'>String BUILD_TYPE</font>** —— build type 的名字，例："release"
* **<font color='green'>String FLAVOR</font>** —— flavor 的名字，例："paidapp"

如果项目使用了 flavor dimensions，会添加额外的值。按照之前的示例，则有如下 BuildConfig：

* **<font color='green'>String FLAVOR = "armFreeapp"</font>**
* **<font color='green'>String FLAVOR_abi = "arm"</font>**
* **<font color='green'>String FLAVOR_version = "freeapp"</font>**