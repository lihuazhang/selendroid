# 系统需求

1. 就如 Junit 一样，Selendroid 可以在 Mac，Linux 和 Windows 上使用。Java 主打的就是跨平台。
2. Java SDK （至少1.6）必须安装。配置 JAVA_HOME 环境变量。 重要： 如果 JAVA_HOME 指向了 JRE（Java runtime environment），Selendroid 会有错误，因为 jarsigner 等工具只有 JDK 下面才有。
3. 请安装最新的 Android-Sdk，配置 ANDROID_HOME 环境变量。
4. 如果你用了 64bit 的 Linux 系统，你需要装下 32 位的架构。
    * sudo dpkg --add-architecture i386
    * sudo apt-get update
    * sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386
5. 模拟器和真机必须有一个。
