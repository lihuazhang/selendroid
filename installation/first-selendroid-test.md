#第一个测试例

测试用例只需遵循 Selenium 2 client API 来写就可以了。 JAVA，Python， Ruby 都可以。

*java 代码*

```java
SelendroidCapabilities capa = new SelendroidCapabilities("io.selendroid.testapp:0.15.0");
WebDriver driver = new SelendroidDriver(capa);
WebElement inputField = driver.findElement(By.id("my_text_field"));
Assert.assertEquals("true", inputField.getAttribute("enabled"));
inputField.sendKeys("Selendroid");
Assert.assertEquals("Selendroid", inputField.getText());
driver.quit();
```

*python 代码*

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

创建一个新的测试 session，需要提供被测应用。被测应用的格式是：**包名:versionName**。如果 versionName 没有提供的话，默认会使用最新版本的应用（这种情况是应用池里有很多不同版本的同一应用。）。然后根据 capabilities 的信息，比如 platformVersion，去设备池里寻找设备。如果找到匹配的模拟器，就启动模拟器或者已经启动了，那就直接使用。如果找到的是真机的话，也是直接使用。这里的匹配非常微妙，如果真机和模拟器同时匹配到了，就会找第一个正在运行的，且不没有在跑测试的机器返回。

在设备初始化完成后，一个经过定制（修改 AndroidManifest.xml 和 换签名）的 selendroid-server 会被自动安装到设备中去。同时被测应用也会自动安装进去。

当整个 session 初始化完成后， 测试命令，比如查找，定位，交互这些都会路由到设备中去。一旦 session 结束，模拟器也会停止。
