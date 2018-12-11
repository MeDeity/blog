#### ImageButton/AppCompatImageButton 按钮

1. 提供了圆形蓝色背景的xml文件

/drawable/image_button_background_blue.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="@color/colorPrimaryDark"/>
</shape>
```

2. 提供了ImageButton按钮的图标,支持在点击的时候显示不同的图标

```xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true" android:drawable="@drawable/ic_flash_on"/>
    <item android:drawable="@drawable/ic_flash_off"/>
</selector>
```
3. 使用
```xml
<android.support.v7.widget.AppCompatImageButton
                android:id="@+id/btn_flash_controller"
                android:layout_width="56dp"
                android:layout_height="56dp"
                android:background="@drawable/image_button_background_blue"
                app:srcCompat="@drawable/btn_flash_selector" />
```
示例效果:
![按钮效果](../../screenshots/image_button_src.png)


>特别注意,在Android 5.0(Android 4.4.4)版本以下使用SVG资源,IDE会报以下的错误:
```java
Caused by: org.xmlpull.v1.XmlPullParserException: 
Binary XML file line #1: invalid drawable tag vector
```

处理方案:
在build.gradle中添加依赖
```
implementation 'com.android.support:support-vector-drawable:xx.x.x'
```

在defaultConfig中添加以下声明
```
defaultConfig {
    ...
    vectorDrawables.useSupportLibrary = true
}
```

1. 使用AppCompat*类代替控件,例如使用AppCompatImageButton代替ImageButton控件实现
2. 使用==app:srcCompat== 代替 android:src
```
<android.support.v7.widget.AppCompatImageButton
    android:id="@+id/btn_flash_controller"
    android:layout_width="56dp"
    android:layout_height="56dp"
    android:background="@drawable/image_button_background_blue"
    app:srcCompat="@drawable/btn_flash_selector" />
```

在Activity或者Fragment页面调用以下语句
AppCompatDelegate.setCompatVectorFromResourcesEnabled(true);
```
static {//5.0以下 svg资源 显示问题修正
    AppCompatDelegate.setCompatVectorFromResourcesEnabled(true);
}
    
 @Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    ...
}
```





