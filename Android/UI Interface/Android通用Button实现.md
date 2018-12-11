#### ImageButton 按钮

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