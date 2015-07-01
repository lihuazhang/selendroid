# Selendroid Server

Selendroid Server 本身是一个 instrumentation，这个就像大家熟悉的 instrumentation 测试里面的测试应用。

1. Selendroid Server 是以一个 **instrumentation apk**
2. 这个 apk 里面起了一个 **HTTP Server**
3. 这个 HttpServer 实现了 Selenium Webdiver 的协议。 从Selendroid Client 过来的请求会映射到各个不同的处理方法中去。
4. 而各个不同的处理方法，则是去通过 instrumentation 这个框架去和设备沟通，得到执行的结果，再由 HttpServer 返回到设备外部。
