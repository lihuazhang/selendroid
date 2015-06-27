# Selendroid Server

Selendroid Server 本身是一个 instrumentation，这个就像大家熟悉的 instrumentation 测试里面的测试应用。

你可以把 Selendroid Server 理解为邮电局里的电报翻译，恰巧这个翻译继承了 instrumentation 的所有功能，更巧的是，这个翻译还是实现了 Selenium Webdriver 的 rest protocol。

在运行客户端用例之前，我们把翻译送到手机设备中去。然后开始运行客户端代码，从 Selendroid Client 送过来的电报，被分发到这个翻译手上。

那这份电报其实走的是 Selenium Webdriver 的电文。所以翻译首先要解码，再翻译成 instrumentation 看得懂的语言，最后由 instrumentation 运行，返回给手机设备外部。

准确点说：

1. Selendroid Server 是以一个 **instrumentation apk。**
2. 这个 apk 里面起了一个 **HTTP Server**。
3. 这个 HttpServer 实现了 Selenium Webdiver 的协议。 Selendroid Client 过来的请求会映射到各个不同的处理方法中去。
