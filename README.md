prevent permission to op sync

make magisk-module

```
adb pull /system/framework/services.jar
apktool.bat d services.jar
```

android 10 : 29.md
android 11 : 30.md

```
apktool.bat b services.jar.out
```

copy services.jar.out/dist/services.jar to magisk-module\system\framework