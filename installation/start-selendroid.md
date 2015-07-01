# 启动 Selendroid

从官方下载到 [selendroid-standalone-version-with-dependencies.jar](https://github.com/selendroid/selendroid/releases/download/0.15.0/selendroid-standalone-0.15.0-with-dependencies.jar) 后，然后直接使用以下命令就可以启动：

```bash
java -jar selendroid-standalone-0.15.0-with-dependencies.jar -app selendroid-test-app-0.15.0.apk
```

目前最新的版本是 0.16.0，稳定版本是 0.15.0。

Selendroid-standalone 会开启一个 http 服务器，在4444端口监听。

Selendroid-standalone server 会维护一个设备池。在服务器启动的时候，搜寻用户创建的所有的虚拟机（~/.android/avd/ 下面的）加入池子。 版本和屏幕信息都会被标识出来。从 0.11.0 版本后，selendroid 可以使用启动好的模拟器，即便是在服务器启动之后再打开的模拟器。如果真机插入的话，也会被加到设备池中去。

