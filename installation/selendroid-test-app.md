# Selendroid 的 AUT

AUT， Application under test。Selendroid 要求被测应用（AUT）必须和 selendroid-standalone server 在一台机器上。

原因就在于  selendroid-standalone server 会做一个和 AUT 同样签名的 Selendroid Server APK 出来，然后再把 AUT 和 Selendroid Server APK 安装到同一台设备中去。

Selendroid 提供了一个被测应用， **selendroid-test-app.apk**。可以用来验证 Selendroid 的各种功能，想玩转 Selendroid 的话，非此 apk 不可。大家可以去官网获取，或者自己编译（自己编译我们后面会讲）。
