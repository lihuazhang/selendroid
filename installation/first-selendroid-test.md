#第一个测试例

测试用例只需遵循 Selenium 2 client API 来写就可以了。 JAVA，Python， Ruby 都可以。

**java 代码**

```java
SelendroidCapabilities capa = new SelendroidCapabilities("io.selendroid.testapp:0.15.0");
WebDriver driver = new SelendroidDriver(capa);
WebElement inputField = driver.findElement(By.id("my_text_field"));
Assert.assertEquals("true", inputField.getAttribute("enabled"));
inputField.sendKeys("Selendroid");
Assert.assertEquals("Selendroid", inputField.getText());
driver.quit();
```

**python 代码**

```python
'''
@author: Dominik Dary
'''
import unittest
from selenium import webdriver


class FindElementTest(unittest.TestCase):

    def setUp(self):
        desired_capabilities = {'aut': 'io.selendroid.testapp:0.10.0'}

        self.driver = webdriver.Remote(
            desired_capabilities=desired_capabilities
        )
        self.driver.implicitly_wait(30)

    def test_find_element_by_id(self):
        self.driver.get('and-activity://io.selendroid.testapp.HomeScreenActivity')
        self.assertTrue("and-activity://HomeScreenActivity" in self.driver.current_url)
        my_text_field = self.driver.find_element_by_id('my_text_field')
        my_text_field.send_keys('Hello Selendroid')

        self.assertTrue('Hello Selendroid' in my_text_field.text)

    def tearDown(self):
        self.driver.quit()

if __name__ == '__main__':
    unittest.main()

```

### Hello, World!

不免俗套，我们使用 selendroid-test-app 来做一个输入 `Hello,World!`，然后验证下输入是否正确。这里我会 step by step 的讲一下。

1. 创建一个 maven 项目。

    无论你是使用 eclipse 还是 intellijidea，创建 maven 项目都应该是你本来就会的。或者你可以直接使用命令行，
    ```bash
     mvn archetype:generate -DgroupId=com.testerhome -DartifactId=helloworld -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
    执行完毕后，我们会看到如下的目录结构：
    ```bash
    ├── pom.xml
    └── src
    ├── main
    │    └── java
    │       └── com
    │           └── testerhome
    │               └── App.java
    └── test
        └── java
            └── com
                └── testerhome
                    └── AppTest.java

    ```

    我们的 pom.xml 如下：

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>testerhome</groupId>
        <artifactId>selendroid_test</artifactId>
        <version>1.0-SNAPSHOT</version>

        <dependencies>
            <dependency>
                <groupId>io.selendroid</groupId>
                <version>0.12.0</version>
                <artifactId>selendroid-standalone</artifactId>
            </dependency>
            <dependency>
                <groupId>io.selendroid</groupId>
                <version>0.12.0</version>
                <artifactId>selendroid-client</artifactId>
            </dependency>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.11</version>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>org.hamcrest</groupId>
                <artifactId>hamcrest-library</artifactId>
                <version>1.3</version>
                <scope>test</scope>
            </dependency>
        </dependencies>
    </project>
    ```

    注意：这边用到了 Selendroid 的两个依赖，一个是standalone，一个是 client。事实上，你并不会用到 standalone 这个包，除非你想在代码中启动或关闭 standalone server。我们一般都在命令行手动启动。

2. `mvn clean install` 把依赖下载过来。
3. 然后打开你喜欢的 IDE 导入项目，就可以开始写脚本。
4. 我们的代码是这样的：

    ```java

        public class SelendroidNativeTest {

        private SelendroidDriver driver = null;
        public static final String NATIVE_APP = "NATIVE_APP";
        protected static final String HOMESCREEN_ACTIVITY = "and-activity://io.selendroid.testapp.HomeScreenActivity";
        protected static final String TOUCH_ACTIVITY = "and-activity://io.selendroid.testapp.TouchGesturesActivity";
        protected void openStartActivity() {
            driver.context(NATIVE_APP);
            driver.get(HOMESCREEN_ACTIVITY);
        }

        @Before
        public void setup() throws Exception {
            DesiredCapabilities cap = new SelendroidCapabilities("io.selendroid.testapp:0.16.0-SNAPSHOT");
            driver = new SelendroidDriver(cap);
            driver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
        }

        @After
        public void teardown() {
            if (driver != null) {
                driver.quit();
            }
        }

        @Test
        public void inputBoxTest() {

            WebElement inputField = driver.findElement(By.id("my_text_field"));
            Assert.assertEquals("true", inputField.getAttribute("enabled"));
            inputField.sendKeys("Hello, World!");
            Assert.assertEquals("Hello, World!", inputField.getText());

        }
    ```
5. 启动 Selendroid-standalone-server：
    ```
    java -jar selendroid-standalone-0.16.0-SNAPSHOT-with-dependencies.jar -app selendroid-test-app-0.16.0-SNAPSHOT.apk
    ```
6. 运行测试用例（Junit 的运行方式）。

### 一个用例的生命过程

创建一个新的测试 session，需要提供被测应用。被测应用的格式是：**包名:versionName**。如果 versionName 没有提供的话，默认会使用最新版本的应用（这种情况是应用池里有很多不同版本的同一应用）。然后根据 capabilities 的信息，比如 platformVersion，去设备池里寻找设备。如果找到匹配的模拟器，就启动模拟器或者已经启动了，那就直接使用。如果找到的是真机的话，也是直接使用。这里的匹配非常微妙，如果真机和模拟器同时匹配到了，就会找第一个正在运行的，且不没有在跑测试的机器返回。

在设备初始化完成后，一个经过定制（修改 AndroidManifest.xml 和 换签名）的 selendroid-server 会被自动安装到设备中去。同时被测应用也会自动安装进去。

当整个 session 初始化完成后， 测试命令，比如查找，定位，交互这些都会路由到设备中去。一旦 session 结束，模拟器也会停止。
