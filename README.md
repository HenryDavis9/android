from appium import webdriver
from appium.webdriver.common.touch_action import TouchAction
import time

# Appium服务器地址和连接参数
appium_server = 'http://localhost:4723/wd/hub'
desired_caps = {
    'platformName': 'Android',
    'deviceName': 'Android Device',
    'appPackage': 'com.example.myapp',  # 替换为您要控制的应用程序包名
    'appActivity': '.MainActivity'  # 替换为您要控制的应用程序主活动名称
}

# 连接到手机应用程序
driver = webdriver.Remote(appium_server, desired_caps)

# 在应用程序中查找元素并执行操作
element = driver.find_element_by_id('com.example.myapp:id/button')  # 替换为您要操作的元素ID
element.click()  # 单击元素

# 执行滑动操作
action = TouchAction(driver)
action.press(x=100, y=500).move_to(x=500, y=500).release().perform()  # 从点(100, 500)滑动到(500, 500)

# 执行输入操作
text_field = driver.find_element_by_id('com.example.myapp:id/textField')  # 替换为您要输入文本的元素ID
text_field.send_keys('Hello, World!')  # 输入文本

# 截图
screenshot = driver.get_screenshot_as_file('screenshot.png')  # 捕捉应用程序截图并保存为文件

# 等待
time.sleep(2)  # 暂停执行2秒

# 断开与手机应用程序的连接
driver.quit()
