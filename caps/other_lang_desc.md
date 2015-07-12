# 其他语言秒速


`SelendroidCapabilities` 在其他语言中是没有实现的，所以其他的语言中就只能使用 Selenium Webdriver 客户端实现的 `DesiredCapabilities`。那说到底，其实就是一个 `key-value` 的 `hash`。

### python

```python
    desired_capabilities = {'aut': 'io.selendroid.testapp:0.10.0'}

    self.driver = webdriver.Remote(
        desired_capabilities=desired_capabilities
    )
    self.driver.implicitly_wait(30)
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
