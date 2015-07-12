#Selendroid-Standalone

在前面两节我们说了，Selendroid Server 和 AndroidDriver 都是 apk，那这些 apk 是怎么被安装到设备中去呢？

Selendroid Server 启动的 HttpServer 在设备中，客户端测试脚本在 PC 机上，他们又是怎么沟通的呢？

客户端脚本怎么知道去哪个设备执行用例呢？

这些问题就要问 Selendroid 的大总管 —— **Selendroid-Standalone**。

Selendroid-Standalone 在 selendroid-client 和 selendroid-server 之间扮演了一个代理的角色。

在执行 Selendroid 测试用例前，我们都需要招呼这个管家起来工作，所以准确来说这个管家主要会做以下几件事：

1. 启动一个 HttpServer，接受来自客户端的请求。
2. 对 selendroid-server，被测应用等 apk 进行统一签名。
3. 根据客户端脚本参数初始化设备，比如和模拟器或者真机建立连接。
4. 安装相关的应用。
5. 将设备上的端口 forward 到 pc 机，打通selendroid-client 和 selendroid-server 之间的通讯。
6. 实现了一些额外的接口，比如通过 adb 执行命令。

另外，大管家还维护两个池子：

1. **deviceStore**： 大管家启动的时候，会找到机器上所有的 android 模拟器和连接的 android 设备，把这些设备信息添加到 deviceStore 中去，以备后续脚本使用。（大管家有两个监听器，分别对模拟器和真机的变化做监听，这样就可以实时更新池子。）

2. **appStore**：我们启动大管家的时候会传 aut 给他，大管家会把这个 aut 加入到 appStore 中去。
