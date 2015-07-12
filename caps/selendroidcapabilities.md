# SelendroidCapabilities


**SelendroidCapabilities** 只有 Java 下才有实现，它继承于 **DesiredCapabilities**，添加了 Android 相关的特性，比如最常用的：

1. 配置 AUT
2. 配置 启动的 Activity
3. 配置 Selendroid Extension
4. 返回 serialNumber
5. 返回手机型号
6. 返回被测应用

另外 SelendroidCapabilities 还提供了一个 `bootstrapClassNames` 的植入，可以帮助用户在应用启动之前做一些操作，当然这个需要配合 Selendroid Extension。



### 设备描述

SelendroidCapabilities 提供了几种默认的配置：

* SelendroidCapabilities.android() 这个配置是使用 selendroid 的 提供的 AndroidDriver app 去测试网页的。（见2-2.3）

  ```java
  public static DesiredCapabilities android(DeviceTargetPlatform platform) {
    SelendroidCapabilities capabilities = new SelendroidCapabilities();
    capabilities.setCapability(BROWSER_NAME, BrowserType.ANDROID);
    capabilities.setCapability(VERSION, "");
    capabilities.setCapability(PLATFORM, "android");
    capabilities.setCapability(PLATFORM_NAME, "android");
    capabilities.setCapability(PLATFORM_VERSION, platform.getApi());
    return capabilities;
  }

  ```

* SelendroidCapabilities.emulator() 这个配置是通过传入的 platform 从设备池中选取匹配的模拟器。

  ```java
  public static SelendroidCapabilities emulator(DeviceTargetPlatform platform, String aut) {
    SelendroidCapabilities caps = new SelendroidCapabilities();
    caps.setPlatformVersion(platform);
    caps.setAut(aut);
    caps.setEmulator(true);
    return caps;
  }
  ```


* SelendroidCapabilities.device() 这个配置是通过传入的 platform 信息去设备池中选取匹配的真机设备。

  ```java
  public static SelendroidCapabilities device(DeviceTargetPlatform platform, String aut) {
    SelendroidCapabilities caps = emulator(platform, aut);
    caps.setEmulator(false);

    return caps;
  }
  ```

默认的配置还是比较死的，所以 Selendroid 还提供了更加灵活的方式 `SelendroidCapabilities( ... )`，比如：

```java
SelendroidCapabilities capa = new SelendroidCapabilities("io.selendroid.testapp:0.8.0");
capa.setPlatformVersion(DeviceTargetPlatform.ANDROID18);
capa.setEmulator(true);
capa.setModel("Nexus 7");
```



