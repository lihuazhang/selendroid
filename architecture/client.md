# Selendroid Client

你可以把 Selendroid Client 看成传统的 **Webdriver Java Client** + **移动特性的实现**。

看下 SelendroidDriver 的实现：
```java
public class SelendroidDriver extends RemoteWebDriver
    implements
      HasTouchScreen,
      HasMultiTouchScreen,
      ScreenBrightness,
      Rotatable,
      Configuration,
      AdbSupport,
      ContextAware,
      SetsSystemProperties,
      CallsGc {……}
```

Selendroid 为在门户网页时代的自动化测试人员提供了无缝的接入。任何一个熟悉 Selenium Webdriver 的人都能轻易上手。
