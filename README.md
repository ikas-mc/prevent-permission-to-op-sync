prevent permission to op sync

update : https://github.com/ikas-mc/Prevent-Op-Sync-Patcher

```java
//PermissionPolicyService.class

private void setUidMode(int opCode, int uid, int mode,
        @NonNull String packageName) {
    final int oldMode = mAppOpsManager.unsafeCheckOpRaw(AppOpsManager.opToPublicName(
            opCode), uid, packageName);
    //add oldMode !=MODE_IGNORED
    //if (oldMode != mode) {
    if (oldMode != mode && oldMode !=MODE_IGNORED) {
        mAppOpsManagerInternal.setUidModeFromPermissionPolicy(opCode, uid, mode,
                mAppOpsCallback);
        final int newMode = mAppOpsManager.unsafeCheckOpRaw(AppOpsManager.opToPublicName(
                opCode), uid, packageName);
        if (newMode != mode) {
            mAppOpsManagerInternal.setModeFromPermissionPolicy(opCode, uid, packageName,
                    AppOpsManager.opToDefaultMode(opCode), mAppOpsCallback);
        }
    }
}
```

make magisk module

```shell
adb pull /system/framework/services.jar
apktool.bat d services.jar
```

android 10 : 29.md

android 11 : 30.md

```shell
apktool.bat b services.jar.out
```

copy services.jar.out/dist/services.jar to magisk-module\system\framework
