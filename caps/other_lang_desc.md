# 其他语言描述


`SelendroidCapabilities` 在其他语言中是没有实现的，所以其他的语言中就只能使用 Selenium Webdriver 客户端实现的 `DesiredCapabilities`。那说到底，其实就是一个 `key-value` 的 `map`。

### python

```python

    desired_capabilities = DesiredCapabilities.android.copy()
    desired_capabilities['aut'] = 'io.selendroid.testapp:0.10.0'
    desired_capabilities['browserName']= 'selendroid'

    self.driver = webdriver.Remote(
        desired_capabilities=desired_capabilities
    )
    self.driver.implicitly_wait(30)
```

selenium python-bindings 里面的 `capabilities.ANDROID` 是一个 map：

```javascript
 {'platform': 'ANDROID', 'browserName': 'android', 'version': '', 'javascriptEnabled': True}

```

### Ruby

```ruby

    require 'selenium-webdriver'
    caps = Selenium::WebDriver::Remote::Capabilities.android
    caps.version = "5"
    caps.platform = :linux
    caps.proxy = nil
    caps[:aut] = "io.selendroid.testapp:0.5.0-SNAPSHOT"
    caps[:locale]="de_DE"
    caps[:browserName]="selendroid"


    @driver = Selenium::WebDriver.for(
    :remote,
    :url => "http://localhost:5555/wd/hub",
    :desired_capabilities => caps)
```

`Selenium::WebDriver::Remote::Capabilities.android` 的实现其实也是一个 hash 而已：

```ruby
# File 'rb/lib/selenium/webdriver/remote/capabilities.rb', line 44

def android(opts = {})
  new({
    :browser_name     => "android",
    :platform         => :android,
    :rotatable        => true,
    :takes_screenshot => true
  }.merge(opts))
end
```

可以看出，无论是 python 还是 ruby，其实就是对一个 map 做文章，根据 selendroid 的需求配置不同的 map，就可以了。

注意： 由于其他语言的实现用的 **browserName** 默认都是 **android**，selendroid 会认为是 androidDriver（见2-2.3）。所以如果你要测试原生应用的话，请覆盖该值。
