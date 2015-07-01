# 启动 Selendroid

从官方下载到 [selendroid-standalone-version-with-dependencies.jar](https://github.com/selendroid/selendroid/releases/download/0.15.0/selendroid-standalone-0.15.0-with-dependencies.jar) 后，然后直接使用以下命令就可以启动：

```bash
java -jar selendroid-standalone-0.15.0-with-dependencies.jar -app selendroid-test-app-0.15.0.apk
```

目前最新的版本是 0.16.0，稳定版本是 0.15.0。

Selendroid-standalone 会开启一个 http 服务器，在4444端口监听。

Selendroid-standalone server 会维护一个设备池。在服务器启动的时候，搜寻用户创建的所有的虚拟机（~/.android/avd/ 下面的）加入池子。 版本和屏幕信息都会被标识出来。从 0.11.0 版本后，selendroid 可以使用启动好的模拟器，即便是在服务器启动之后再打开的模拟器。如果真机插入的话，也会被加到设备池中去。

你可以通过 http://localhost:4444/wd/hub/status 来检查应用和设备，比如：

```java
{
value: {
os: {
name: "Mac OS X",
        arch: "x86_64",
        version: "10.10.3"
    },
build: {
browserName: "selendroid",
             version: "0.16.0-SNAPSHOT"
       },
supportedDevices: [
                  {
emulator: true,
          screenSize: "(768, 1280)",
          avdName: "4.2",
          platformVersion: "17"
                  },
                  {
emulator: true,
          screenSize: "(768, 1280)",
          avdName: "4.4.2",
          platformVersion: "19"
                  },
                  {
emulator: false,
          screenSize: "(1080, 1920)",
          serial: "02523b04",
          platformVersion: "19",
          model: "MI 3"
                  },
                  {
emulator: true,
          screenSize: "(480, 800)",
          avdName: "4.0.3",
          platformVersion: "15"
                  },
                  {
emulator: true,
          screenSize: "(320, 480)",
          avdName: "4.1",
          platformVersion: "16"
                  }
    ],
      supportedApps: [
      {
        mainActivity: "io.selendroid.androiddriver.WebViewActivity",
        appId: "io.selendroid.androiddriver:0.16.0-SNAPSHOT",
        basePackage: "io.selendroid.androiddriver"
  }
    ]
       },
status: 0
}

```

不难看出，我使用的是 0.16.0 版本，启动的时候就把模拟器都找出来了，而其中的小米3手机，则是启动之后，插上去的。那在 supportedApps 里面，则是我启动时候带上的 AUT。

所以我的启动命令是这样的：

```bash
 java -jar selendroid-standalone-0.16.0-SNAPSHOT-with-dependencies.jar -app ../../selendroid-test-app/target/selendroid-test-app-0.16.0-SNAPSHOT.apk
```

其实启动的时候有很多参数选项。

### 启动参数

**-h, --help**

打印帮助信息

**-port**

指定监听端口，默认 4444

** -app， -aut**

指定 AUT，绝对路径

**-timeoutEmulatorStart**

指定模拟器启动的超时时间，单位毫秒，默认是 300，000 毫秒（5分钟）

**-emulatorPort**

模拟器的端口（一般模拟器都是5555）

**-deviceScreenshot**

激活 screenshots 来截图，而不是通过 ddmlib

**-selendroidServerPort**

指定 selendroid-standalone 和 设备内部的 selendroid server 沟通的端口，默认是 8080

**-deviceLog**

是否激活 adb 日志。

**-logLevel**

指定日志级别，默认是：ERROR，可选有：ERROR，WARNING，INFO，DEBUG 和 VERBOSE

**-keystore**

指定签名用的 keystore

**-keystoreAlias**

keystore的别名

**-keystorePassword**

keystore 的密码

**-emulatorOptions**

指定模拟器启动时候的选项，比如：-no-audio

**-noWebviewApp**

设置了该选项，那么 Selendroid 不会自动安装 *AndroidDriver*

**-noClearData**

指定是否要在每个测试 session 结束后，清空用户数据

**-sessionTimeout**

指定 session 的超时时间，单位为秒。默认30分钟，如果超时，会强制关闭 session

**-serverStartTimeout**

设备内部 selendroid-server 启动的超时时间，默认 20000 毫秒

**-keepAdbAlive**

如果指定该选项，那么服务关闭后，adb 不会被关闭。

**-hub**

指定 Selenium grid hub 的 url，比如：http://localhost:4444/grid/register

**-proxy**

指定 Selenium grid hub 的远端代理，比如：io.selendroid.grid.SelendroidSessionProxy

**-host**

指定节点的 host。这些都是 grid 时候用到的

**-folder**

指定一个文件夹的绝对路径，来监控新的应用，以便添加到应用池里。（通常不需要）
