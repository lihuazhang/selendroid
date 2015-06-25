# 什么是 Selendroid

### 简介

Selendroid 是一个测试自动化框架，支持 Android 的原生应用，混合应用和移动 Web。软件测试工程师可以使用 Selenium 2 的客户端 API 来写自动化测试脚本。

Selendroid 由 **eBay Software Foundation** 发起，是一个开源项目，由众多人士支持。目前代码 base 在 [github](https://github.com/selendroid/selendroid) 上。

### 支持的设备
Selendroid 支持且仅支持 Android 的模拟器和真机。同时可以集成到 Selenium Grid 中去进行大规模或者并发测试。

如果想用 Webdriver 来测试 iOS 的原生应用，混合应用和移动 Web的话，我们推荐 [ios-driver](http://ios-driver.github.io/ios-driver/)。

### 特性

* 完全兼容 Webdriver 的 JSON Wire Protocol
* 不需要为了自动化修改被测应用
* 使用一个 Android webview 应用来测试移动网页
* 原生和混合应用自动化采用同样的理念
* 使用不同的定位方式来查找 UI 元素
* 支持手势：[高级用户交互接口](http://selendroid.io/gestures.html)
* Selendroid 可以同时和多台设备（模拟器或者真机）交互
* 可以自动启动模拟器
* 支持真机热插拔
* 可以充当一个节点完全整合进 Selenium Grid，进行大规模和并发测试。
* 支持多个 Android API （10到19）
* 提供 Inspector 简化测试脚本开发
* 可以扩展自己的插件！


