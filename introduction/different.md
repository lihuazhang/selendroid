# Selendroid 和其他框架的区别

Android 基于 UI 层面的自动化测试工具，都可以理解为是基于 **Android 控件**层面的，涉及**原生控件**和 **WebView** 两大类。

目前主流的测试方法主要有以下几种：

1. 通过 Android 提供的各种服务，来获取当前窗口的视图信息（通常是 dump 布局控件为 xml 文件）。然后，在当前视图内查找目标控件，并根据该控件属性信息计算出该控件中心点的坐标，进而构造出一个 Android Input 事件来实现对应用的自动化测试。其主要特点是：测试代码和被测应用各自运行在各自的进程内，相互独立。其代表有 Uiautomator。

2. 基于 Instrumentation，通过把测试代码和应用代码，确切地说是测试 APK 和被测 APK，运行在同一个进程中，通过 Java 反射机制，来获取当前窗口所有视图，并根据该视图查找到目标控件的属性信息，并计算出目标控件中心点坐标。然后，利用 Instrument 内部接口，实现点击操作。其代表有 Robotium。

Selendroid 属于第二种，基于 Instrumentation。那么什么是 Instrumentation？

>This object is natively to the Java language, but in Android it has the main role of controlling the life cycle of an application. An Android application has specific life cycle that cannot be broken.The instrumentation has an ability to run code before each one of these events. This ability is used to inject relevant test code and allow test automation.
![](/imgs/instrumentation.png)



简单来说， instrumentation 通过插入安卓应用的生命周期来注入自动化行为。所以这也注定了 Selendroid 框架的一些特点：

1. 被测应用需要和 Selendroid Server 统一签名
2. 无法跨应用

网上有人总结了以下的表格：

|  | Hierachyview+MonkeyRunner| UiAutomator 系列 | Instrumentation 系列 |
| -- | -- | -- | -- |
| 权限 | root | 普通 | 普通 |
| 是否需要签名 | 是 | 否 | 是 |
| 响应速度 | 10s（网友测试数据） | 4s（网友测试数据） | 1-2s |
| 是否支持WebView | 否 | 否 | 是 |
| 是否支持跨应用测试 | 是 | 是 | 否 |
| 支持该特性的Android API | ？ | API16 | API7 |
| 是否支持控件ID | 是 | 否 | 是 |

显而易见，Selendroid 作为 Android 自动化测试框架的一员，还是非常强大的（当然比不过 Appium 那样的庞然大物）。
