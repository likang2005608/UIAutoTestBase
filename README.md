# UIAutoTestBase
UI自动化测试基础知识点

# 元素的定位的8种方法
①id

②name

③class name

④tag name

⑤link text

⑥partial link text

⑦xpath

⑧CSS

如果实在不知道怎么通过上述8个类型去定位，那么可以再在火狐浏览器47版本及以下装一个firebug和Xpath来快速的获取元素的定位
基本语法：find_element_by_xpath("//input[@id=‘kw’]")

# 操作浏览器界面
①全屏：maximize_window()，无需传参
例：driver.maximize_window()

②指定大小：set_window_size(宽，高)
例：driver.set_window_size(480, 800)

③控制浏览器前进：forward()
例：driver.forward()

④控制浏览器后退：back()

⑤关闭标签页:driver.close()

⑥关闭浏览器:driver.quit()

# 元素的基本操作
①clear() 清除文本，如果是一个文件输入框
例：driver.find_element_by_id(“idInput”).clear()

②send_keys(*value) 在元素上模拟按键输入
例：driver.find_element_by_id(“idInput”).send_keys(“username”)

③click() 单击元素
例：driver.find_element_by_id(“loginBtn”).click()

④submit()方法用于提交表单，这里特别用于没提交按钮的情况，例如搜索框输入关键字之后的“回车”操作，那么就可以通过 submit()来提交搜索框的内容。
例：driver.find_element_by_id(‘query’).submit()

⑤size 返回元素的尺寸。
例：size=driver.find_element_by_id(‘kw’).size
print size

⑥text 获取元素的文本。
text=driver.find_element_by_id(“cp”).text
print text

⑦get_attribute(name) 获得属性值。
例：attribute=driver.find_element_by_id(“kw”).get_attribute(‘type’)
print attribute

⑧is_displayed() 设置该元素是否用户可见。
例：result=driver.find_element_by_id(“kw”).is_displayed()
print result

# 鼠标操作事件
如：A=driver.find_element_by_id(“cp”)
①ActionChains(driver).context_click(A).perform() # 右键

②ActionChains(driver).double_click(A).perform() # 双击

③ActionChains(driver).move_to_element(A).perform() # 鼠标悬停

④ActionChains(driver).drag_and_drop(A, target).perform() # 将source元素拖拽到target元素位

⑤ActionChains(driver).drag_and_drop(A, x, y).perform() # 将source元素相对于自己的位置拖拽

注：鼠标操作的方法由 ActionChains 类提供
perform() 执行所有 ActionChains 中存储的行为

# 键盘事件
driver.find_element_by_id(“kw”).send_keys(“seleniumm”) # 输入内容selenium

driver.find_element_by_id(“kw”).send_keys(Keys.BACK_SPACE) # 退格

driver.find_element_by_id(“kw”).send_keys(Keys.SPACE) # 空格键

driver.find_element_by_id(“kw”).send_keys(Keys.CONTROL,‘a’) # 全选输入框内容

driver.find_element_by_id(“kw”).send_keys(Keys.CONTROL,‘x’) # 剪切输入框内容

driver.find_element_by_id(“kw”).send_keys(Keys.CONTROL,‘v’) # 粘贴内容到输入框

driver.find_element_by_id(“kw”).send_keys(Keys.CONTROL,‘c’) # 复制选中的内容

driver.find_element_by_id(“su”).send_keys(Keys.ENTER) # 回车操作代替点击按钮

driver.find_element_by_id(“su”).send_keys(Keys.ESCAPE) # 退出按钮

driver.find_element_by_id(“su”).send_keys(Keys.TAB) # 制表键

driver.find_element_by_id(“su”).send_keys(Keys.F1) # 按下键盘F1

# 等待函数
①driver.implicitly_wait(10) # 等待10秒钟，若提前结束就停止等待，若超时就抛出异常
②time.sleep(10) # 傻傻的等待10秒钟，不管是否提前结束

# 不同框架之间的切换
①driver.switch_to.frame(“if”) # 切换到id或者name为if的框架

②driver.switch_to.frame(frame) 若无法用name 或者 id定位到框架，则可以先用其他方式定位获取到框架元素，再将这个元素传入switch_to…frame()里，如：
1）xf = driver.find_element_by_xpath(’//*[@class=“if”]’)
2）#再将定位对象传给 switch_to_frame()方法
driver.switch_to_frame(xf)

③driver.switch_to_default.content() # 切换到默认的框架中

# 不同窗口的切换（弹框）
①driver.current_window_handle # 获取当前窗口的句柄，切换到js弹框上

②driver.window_handles 　　 # 获取所有窗口的句柄

③driver.switch_to.window() 　 # 切换到某个窗口

# 警告弹框的处理
①driver.switch_to.alert() # 切换到弹框（alert、prompt、confirm）

②driver.switch_to.alert().text # 获取弹框的文本内容

③driver.switch_to_alert().accept()　 # 切换到弹框并且点击“确认”

④driver.switch_to.alert().dismiss() # 切换到弹框并且点击“取消”

⑤driver.switch_to.alert().sendkeys(‘hello’) # 切换到弹框并且在输入框中输

# 文件上传
#打开上传功能页面
file_path = ‘file:///’ + os.path.abspath(‘upfile.html’)
driver.get(file_path)

#定位上传按钮，添加本地文件
driver.find_element_by_name(“file”).send_keys(‘D:\upload_file.txt’)

# 调用JS
①js=“var q=document.documentElement.scrollTop=10000”

编写js代码：将页面的滚动条向下移动10000px
driver.execute_script(js)
#执行上面的JS语句

②#将页面滚动条拖到底部
js=“var q=document.documentElement.scrollTop=10000”
driver.execute_script(js)
time.sleep(3)

③#将滚动条移动到页面的顶部
js_=“var q=document.documentElement.scrollTop=0”
driver.execute_script(js_)
time.sleep(3)

# 错误窗口截图
driver.get_screenshot_as_file(“D:\baidu_error.jpg”)
将当前页面可视区截图并存放命名为D:\baidu_error.jpg

例:
driver.get(‘http://www.baidu.com’)
try:
driver.find_element_by_id(‘kw_error’).send_key(‘selenium’)
driver.find_element_by_id(‘su’).click()
except :
driver.get_screenshot_as_file(“D:\baidu_error.jpg”)
driver.quit()
