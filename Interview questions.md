【50+道自动化/Selenium/性能/Python面试题】

蛋糕不加蛋  51Testing软件测试圈  6月23日




写在前面

公司要求招一名自动化测试，能力要求不高，1年左右自动化经验+部分性能经验即可，让我出一份题，我就百度+公司项目遇到的问题，出了一份，出题整体思路是：接口自动化问题+性能问题+规划的ui、app自动化+整体质量体系建设等多方面考虑。下面是正题。



岗位JD





# 【自动化测试基础篇】

目的：验证求职者是否在自动化测试岗位有实际应用于生产的工作经验

1、使用什么测试框架做的上一个项目的自动化测试？说下怎么做的？对自动化的理解？

答：（junit、unittest、testng、 pytest ，优先python语言，用过pytest或unittest框架的；只会selenium能力较弱）

2、使用什么测试框架做的上一个项目的自动化测试？说下怎么做的？对自动化的理解？

答：最好能答出独立负责且封装页面元素、断言封装、请求封装、取参方式具体实现

3、GET与POST的区别？

（1）GET请求资源数据，POST向服务器传递需要处理的数据

（2）GET传递数据大小不超过2kb，POST没有限制

（3）GET请求的参数会在Url上暴露显示，POST请求参数在Requestbody里，所以相对GET来说，POST安全性较高

（4）GET 请求的静态资源会被浏览器缓存，POST不会被缓存

（5）GET传递的数据类型是文本，POST是文本或者二进制

（6）GET请求被回退时是无害的，POST请求被回退是会被重新再执行一次

GET和POST的使用场景：

（1）在传递一些机密信息时必须要使用POST

（2）只是查询获取数据时可以用GET

（3）POST请求速率会比GET慢，因为GET请求产生一个TCP数据包;POST请求产生两个TCP数据包

4、//*[contains(@text,“登录”)] 是什么意思？

答：查包含登录关键字的所有元素

5、自动化遇到用例fail掉如何排查故障？

答：看出错log，如果能按层次说清楚排查失败：手工查应用是否真的有bug, 确认不是bug，是不是新版本引入了新的变更，调试脚本看看自己的脚本是不是因为没有等待元素出现后就操作了，是不是元素上面有其他元素出现这样操作是不是操作了其他的元素上了。

6、说说接口测试的流程和接口自动化流程，介绍一下request有哪些内容？

答：
（1）流程：获取接口文档，依据文档设计接口参数，获取响应，解析响应，校验结果，判断测试是否通过。
（2）request 内容：
1，封装了get、post等；
2、以关键字参数的方式，封装了各类请求参数，params、data、headers、token、cookie等；
3，封装了响应内容，status_code、json()、cookies、url等；session会话对象，可以跨请求。

7、接口测试用例的编写要点有哪些？

1）必填字段：请求参数必填项、可选项
2）合法性：输入输出合法、非法参数
3）边界：请求参数边界值等
4）容错能力：大容量数据、频繁请求、重复请求（如：订单）、异常网络等的处理
5）响应数据校验：断言、数据提取传递到下一级接口…
6）逻辑校验：如两个请求的接口有严格的先后顺序，需要测试调转顺序的情况
7）性能：对接口模拟并发测试，逐步加压，分析瓶颈点
8）安全性：构造恶意的字符请求，如：SQL注入、XSS、敏感信息、业务逻辑（如：跳过某些关键步骤；未经验证操纵敏感数据）

8、postman的使用方式？高级用法？mock的应用场景和基础用法？

答：A，基础使用：入参出参校验返回；
b，Environment–配置不同的环境参数，Globals即设置全局变量，Pre-request Script–配置使用环境变量或进行前置脚本处理；
c，团队可以更好地并行工作，前后端人员只需要定义好接口文档就可以开始并行工作，互不影响，只在最后的联调阶段往来密切，开启TDD（Test-Driven Development）模式，即测试驱动开发

9、你之前自动化测试的数据放哪？怎么使用？公共变量的管理方式？管理测试用例的手段？如何提高用例覆盖率？接口测试关联性接口实现方式？

答：测试数据存放总结：
1.对于账号密码，这种管全局的参数，可以用命令行参数，单独抽出来，写的配置文件里（如ini）
2.对于一些一次性消耗的数据，比如注册，每次注册不一样的数，可以用随机函数生成
3.对于一个接口有多组测试的参数，可以参数化，数据放yaml,text,json,excel都可以
4.对于可以反复使用的数据，比如订单的各种状态需要造数据的情况，可以放到数据库，每次数据初始化，用完后再清理
5.对于邮箱配置的一些参数，可以用ini配置文件
6.对于全部是独立的接口项目，可以用数据驱动方式，用excel/csv管理测试的接口数据
7.对于少量的静态数据，比如一个接口的测试数据，也就2-3组，可以写到py脚本的开头，十年八年都不会变更的。

10、不可逆的操作，如何处理，比如删除一个订单这种接口如何测试？
此题考的是造数据的能力，接口的请求数据，很多都是需要依赖前面一个状态的，比如工作流这种，流向不同的人状态不一样，操作权限不一样，测试的时候，每种状态都要测到,就需要自己会造数据了。
平常手工测试造数据，直接在数据库改字段状态。那么自动化也是一样，造数据可以用python连数据库了，做增删改查的操作测试用例前置操作，setUp做数据准备后置操作，tearDown做数据清理。

11、说出5个以上 Linux 命令（注重考察性能测试监控常用命令？）
答：cd、ls、grep、mkdir、pwd、ping等等，重要是性能测试常用监控命令：netstat 、top 、Nmon 、dstat、ulimit、vmstat 、tcpdump、free 、lsof ，需回答上至少两个。

12、介绍一下你在这个项目中是如何使用 Jenkins 的。
答：基本操作，比如定时构建执行代码等。

13、举例说明，Linux下命令行cURL的种常见用法和示例？
答：常用10种，这里举出三种常用：
A，获取页面内容：curl+get请求；curl
B，把链接页面的内容输出到本地文件中：curl https://www.baidu.com > index.html
C，使用 -d 发送 POST 请求：curl -d “userName=tom&passwd=123456” 

14，jmeter上一个接口参数返回值做为下一个接口入参的实现方式有几种，举例？
答：正则表达式处理器、JSON Path Extractor

15、接口自动化中，遇到签名、鉴权加密等，如何处理的，用到哪些方法？
答：比如MD5加密–hashlib内置库，看怎么回答怎么具体问：开放性。

16、对pytest的理解程度？使用规范？参数化方法？说说常用装饰器？
答：pytest是一个非常成熟的全功能的的Python测试框架，主要特点有以下几点：
1，简单灵活，容易上手，文档丰富;
2，支持参数化，可以细粒度地控制要测试的测试用例;
3，能够支持简单的单元测试和复杂的功能测试，还可以用来做selenium/ appnium等自动化测试，接口自动化测试（pytest +请求）;
4，pytest具有很多第三方插件，并且可以自定义扩展，比较好用的如pytest - selenium（集成selenium），pytest-HTML（完美的HTML测试报告生成），pytest-rerunfailures（失败情况下重复执行），pytest -xdist（多CPU分发）等;
5，测试用例的跳跃和xfail处理；
使用规范：
测试文件名必须以“test_”开头
测试类以Test开头，并且不能带有 init 方法
测试方法必须以“test_”开头
除了有setup/teardown，还能更自由的定义fixture装载测试用例
参数化方法：
pytest支持在多个完整测试参数化方法:
pytest.fixture(): 在fixture级别的function处参数化
@pytest.mark.parametrize：允许在function或class级别的参数化,为特定的测试函数或类提供了多个argument/fixture设置。
pytest_generate_tests：可以实现自己的自定义动态参数化方案或扩展。

17、举例说明pytest.mark标记的使用？
答：1，无条件跳过测试pytest.mark.skip
2，有条件跳过测试pytest.mark.skipif
3，标记测试功能按预期失败pytest.mark.xfail
4，将测试功能标记为使用给定的夹具名称pytest.mark.usefixtures
5，向特定测试项添加警告过滤器，以便更好地控制应在测试，类甚至模块级别捕获哪些警告@pytest.mark.filterwarnings
6，自定义标记：标记指定标签

18，自动化测试报告生成方式？如果是allure详述？
答：@allure.severity(“critical”) # 优先级，包含blocker, critical, normal, minor, trivial 几个不同的等级
@allure.feature(“测试模块_demo1”) # 功能块，feature功能分块时比story大,即同时存在feature和story时,feature为父节点
@allure.story(“测试模块_demo2”) # 功能块，具有相同feature或story的用例将规整到相同模块下,执行时可用于筛选
@allure.issue(“BUG号：123”) # 问题表识，关联标识已有的问题，可为一个url链接地址
@allure.testcase(“用例名：测试字符串相等”) # 用例标识，关联标识用例，可为一个url链接地址

19、什么是冒泡排序，手写一个冒泡排序？
答：冒泡排序（Bubble Sort）也是一种简单直观的排序算法。它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢"浮"到数列的顶端。



# 【语言篇之Python】

目的：验证求职者自动化岗位的开发、脚本语言的基础以及熟悉程度

1、super 是干嘛用的？在 Python2 和 Python3 使用，有什么区别？为什么要使用 super？请举例说明。
答：super 用于继承父类的方法、属性。super 是新式类中才有的，所以 Python2 中使用时，要在类名的参数中写 Object。Python3 默认是新式类，不用写，直接可用。使用 super 可以提高代码的复用性、可维护性。修改代码时，只需修改一处。

2、L = [1, 2, 3, 11, 2, 5, 3, 2, 5, 3]，用一行代码得出 [11, 1, 2, 3, 5]
答：list(set(L))

3、列表和字典有什么区别？
答：一般都是问列表和元组有什么不同。
（1）获取元素的方式不同。列表通过索引值获取，字典通过键获取。（2）数据结构和算法不同。字典是 hash 算法，搜索的速度特别快。（3）占用的内存不同。

4、json和字典dict的区别？
答：json是一种轻量级的数据交换格式
dict是python中的数据类型（python里面的基础数据类型有：int、str、 float、list、bool、tuple、dict、set这几种类型，里面没json这种数据类型，json本质上字符串，按照key:value键值对格式的字符串；在json中空值是用Null表示，在dict中空值是用None表示）
主要区别：json的key只能是字符串，python的dict可以是任何可hash对象（hashtable type）；
json的key可以是有序、重复的；dict的key不可以重复。
json的value只能是字符串、浮点数、布尔值或者null，或者它们构成的数组或者对象。
json任意key存在默认值undefined，dict默认没有默认值；
json访问方式可以是[],也可以是.，遍历方式分in、of；dict的value仅可以下标访问。
json的字符串强制双引号，dict字符串可以单引号、双引号；
dict可以嵌套tuple，json里只有数组。
json:true、false、null
python：True、False、None
json中文必须是unicode编码，如"\u6211".
json的类型是字符串，字典的类型是字典。

5、python深拷贝和浅拷贝的概念和区别？
答：浅拷贝：拷贝最外层容器
深拷贝：拷贝的最外层容器，还拷贝容器中的元素
对于不可变元素，使用浅拷贝

6、python单行注释和多行注释分别用什么？
答：单行注释用# 多行注释用""" “”"

7、Python垃圾回收机制？
答：1，回收计数引用为0的对象，释放其占用空间
2、循环垃圾回收器。释放循环引用对象

8、如何安装第三方模块？以及用过哪些第三方模块？
答：使用官方推荐的setuptools的包管理工具，easy – install和pip、requests模块

9、进程、线程有什么区别？什么情况下用进程？什么情况下用线程？
答：（1）区别：
① 地址空间和其它资源（如打开文件）：进程之间相互独立，同一进程的各线程之间共享。某进程内的线程在其它进程不可见。
② 通信：进程间通信 IPC，线程间可以直接读写进程数据段（如全局变量）来进行通信——需要进程同步和互斥手段的辅助，以保证数据的一致性。
③ 调度和切换：线程上下文切换比进程上下文切换要快得多。
④ 在多线程操作系统中，进程不是一个可执行的实体。
（2）使用场景：同时操作一个对象的时候，比如操作的是一个全局变量，我用线程，因为全局变量是所有线程共享的。

10、谈谈你对面向对象的理解？
答：体现在三个方面：封装、继承、多态
继承有两种方式：
1、将同一类的方法封装到类中
2、将数据封装到对象中
继承：子类拥有父类的所有方法和属性，
好处：抽取重复代码，减少代码冗余。
坏处：耦合性太强。
多态：对于不同的类可以有同名的方法，同名的方法应用到不同的类可以有不同行为。



# 【细节篇之Selenium】

目的：验证求职者在自动化测试岗位的selenium工具的熟悉程度

1、selenium中如何判断元素是否存在？
答：isElementPresent

2、selenium中hidden或者是display ＝ none的元素是否可以定位到？
答：a、可以：定位是可以定位到的，但是不能操作，可以判断元素is_displayed()
想点击的话，可以用js去掉dispalay=none的属性；
b、不能：可以写JavaScript将标签中的hidden先改为0，再定位元素。两个答案都算对，说明出原因即可。

3、selenium中如何保证操作元素的成功率？也就是说如何保证我点击的元素一定是可以点击的？
答：添加元素智能等待时间 driver.implicitly_wait(30)
添加强制等待时间(比如python中写 sleep)
try 方式进行 id,name,clas,x path, css selector 不同方式进行定位，如果第一种失败可以自动尝试第二种。

4、如何提高selenium脚本的执行速度？
答：1.少用sleep，尽量不用implicitly_wait
2.多用显式等待方法
3.弄个性能好的电脑具体？（看个人思路）

5、点击链接以后，selenium是否需要自动等待该页面加载完毕？
答：需要

6、你的自动化用例的执行策略是什么？
答：自动化测试与软件开发本质上是一样的，利用自动化测试工具，经过测试需求分析，设计出自动化测试用例，从而搭建自动化测试的框架，设计与编写自动化脚本，验证测试脚本的正确性，最终完成自动化测试测试脚本（即主要功能为测试的应用软件）并输出测试结果。

7、什么是持续集成？
答：持续集成是一种软件开发实践，即团队开发成员经常集成它们的工作，通过每个成员每天至少集成一次，也就意味着每天可能会发生多次集成。
每次集成都通过自动化的构建（包括编译，发布，自动化测试）来验证，从而尽早地发现集成错误。

8、自动化测试的时候是不是需要连接数据库做数据校验？
答：一般来说：
1、 UI自动化不需要（很少需要）；
2、接口测试会需要：从数据库层面来进行数据校验可以更方便验证系统的数据处理方面是否正确；

9、有几种元素常用定位方式，分别是？你最偏爱哪一种，为什么？
答：8种：id、name、class name、tag name、link text、partial link text、xpath、css selector
偏爱哪一种？xpath、css几乎所有的元素都可以定位到,但是它们的短处在于页面上更改了元素后位置很容易改变，且xpath语法长，定位慢，还不稳定；css语法简洁，定位快，瑕不掩瑜，所以首先使用的还是id或者name、css等。

10、如何去定位页面上动态加载的元素？
答：1，触发动态加载元素的事件，直至动态元素出现，进行定位
2，WebDriverWait（）方法循环去查询是否元素加载出来了

11、如何去定位属性动态变化的元素？
答：xpath或者css通过同级、父级、子级进行定位

12、webdriver client的原理是什么？
答：Selenium RC的原理是当浏览器启动时，向其中注入Javascript，从而使这些JS来驱动浏览器中的AUT(Application Under Test),而Selenium Webdriver是通过调用浏览器原生的自动化API直接驱动浏览器。

13、什么是page object设计模式？
答：简单来说，就是把页面作为对象，在使用中传递页面对象，来使用页面对象中相应的成员或者方法，能更好的体现面向对象语言（比如java或者python）的面向对象和封装特性。

14、什么是断言（assert），常用断言方法，UI自动化中断言方式？
答：断言的英文是assertion，断言检查的英文是assertion checking。
断言是指定一个程序必须已经存在的状态的一个逻辑表达式，或者一组程序变量在程序执行期间的某个点上必须满足的条件，UI自动化中断言方式：定位页面当前页面或跳转页面中元素唯一的一个或多个元素判断是否存在，即可。

15、你觉得自动化测试最大的缺陷是什么？
答：不稳定、可靠性、不易维护、成本与收益。

16、什么是分层测试？
答：行业里面提的一般是金字塔的分层模型：UI测试、集成/接口测试、单元测试。



# 【细节篇之性能篇】

目的：验证求职者在性能测试方面熟悉程度

1、基础概念：HPS、TPS、QPS、RPS、RT、并发用户数概念？简要介绍？
HPS（Hits Per Second）：每秒点击次数，单位是次/秒。
TPS（Transaction per Second）：系统每秒处理事务数，简称TPS, 每秒事务数, 是衡量系统性能的一个非常重要的指标。
QPS（Query per Second）：系统每秒处理查询次数，单位是次/秒。对于互联网业务中，如果某些业务有且仅有一个请求连接，那么TPS=QPS=HPS，一般情况下用TPS来衡量整个业务流程，用QPS来衡量接口查询次数，用HPS来表示对服务器点击请求
RPS 即每秒请求数（Request Per Second），通常用来描述施压引擎实际发出的压力大小。
PS：并发数过低时可能达不到预期的 RPS，并发数过高时可能压力过大压垮服务器
并发用户数：简称VU ,指的是现实系统中操作业务的用户，在性能测试工具中，一般称为虚拟用户数(Virutal User)，注意并发用户数跟注册用户数、在线用户数有很大差别的，并发用户数一定会对服务器产生压力的，而在线用户数只是 ”挂” 在系统上，对服务器不产生压力，注册用户数一般指的是数据库中存在的用户数。
响应时间：简称RT,指的是业务从客户端发起到客户端接受的时间。

2、压测工具？你主要看哪些指标？
答：jmeter：
Label：每个 JMeter 的 element（例如 HTTP Request）都有一个 Name 属性，这里显示的就是 Name 属性的值
#Samples：表示你这次测试中一共发出了多少个请求，如果模拟10个用户，每个用户迭代10次，那么这里显示100
Average：平均响应时间——默认情况下是单个 Request 的平均响应时间，当使用了 Transaction Controller 时，也可以以Transaction 为单位显示平均响应时间
Median：中位数，也就是 50％ 用户的响应时间
90% Line：90％ 用户的响应时间
Note：关于 50％ 和 90％ 并发用户数的含义
Min：最小响应时间
Max：最大响应时间
Error%：本次测试中出现错误的请求的数量/请求的总数
Throughput：吞吐量——默认情况下表示每秒完成的请求数（Request per Second），当使用了 Transaction Controller 时，也可以表示类似 LoadRunner 的 Transaction per Second 数
KB/Sec：每秒从服务器端接收到的数据量，相当于LoadRunner中的Throughput/Sec

3、性能测试中TPS上不去的几种原因浅析？
TPS（Transaction Per Second）：每秒事务数，指服务器在单位时间内（秒）可以处理的事务数量，一般以request/second为单位。
a、网络带宽 
在压力测试中，有时候要模拟大量的用户请求，如果单位时间内传递的数据包过大，超过了带宽的传输能力，那么就会造成网络资源竞争，间接导致服务端接收到的请求数达不到服务端的处理能力上限。
b、连接池
可用的连接数太少，造成请求等待。连接池一般分为服务器连接池（比如Tomcat）和数据库连接池（或者理解为最大允许连接数也行）。
c、垃圾回收机制
从常见的应用服务器来说，比如Tomcat，因为java的的堆栈内存是动态分配，具体的回收机制是基于算法，如果新生代的Eden和Survivor区频繁的进行Minor GC，老年代的full GC也回收较频繁，那么对TPS也是有一定影响的，因为垃圾回收其本身就会占用一定的资源。
d、数据库配置
高并发情况下，如果请求数据需要写入数据库，且需要写入多个表的时候，如果数据库的最大连接数不够，或者写入数据的SQL没有索引没有绑定变量，抑或没有主从分离、读写分离等，就会导致数据库事务处理过慢，影响到TPS。
e、通信连接机制
串行、并行、长连接、管道连接等，不同的连接情况，也间接的会对TPS造成影响。
f、硬件资源
包括CPU（配置、使用率等）、内存（占用率等）、磁盘（I/O、页交换等）。
g、压力机
比如jmeter，单机负载能力有限，如果需要模拟的用户请求数超过其负载极限，也会间接影响TPS（这个时候就需要进行分布式压测来解决其单机负载的问题）。
h、压测脚本
还是以jemter举个例子，之前工作中同事遇到的，进行阶梯式加压测试，最大的模拟请求数超过了设置的线程数，导致线程不足。
提到这个原因，想表达意思是：有时候测试脚本参数配置等原因，也会影响测试结果。
i、业务逻辑
业务解耦度较低，较为复杂，整个事务处理线被拉长导致的问题。
j、系统架构
比如是否有缓存服务，缓存服务器配置，缓存命中率、缓存穿透以及缓存过期等，都会影响到测试结果。

4、性能测试工具了解几个？压测结果区别？
A，ab，是apache自带的压力测试工具
B，Jmeter 基于Java的压力测试工具
c，Locust是一个Python编写的分布式的性能测试工具

5、性能测试策略？
做性能测试需要一套标准化流程及测试策略。在做负载测试的时候，传统方式一般都是按照梯度施压的方式去加用户数，避免在没有预估的情况下，一次加几万个用户，导致交易失败率非常高，响应时间非常长，已经超过了使用者忍受范围内；较为适合互联网分布式架构的方式，是用TPS模式（吞吐量模式）+设置起始和目标最大量级，然后根据系统表现灵活的手工实时调速，效率更高，服务端吞吐能力的衡量一步到位。

6、性能测试场景设置思路？
无论并发模式还是TPS模式，场景就是一个压测模型，压测模型中有串行的事务（如添加购物车+购物车下单+付款）也有并行的接口（在不同串联链路中的压测API），最终组成一个复杂或者简单的场景。然后根据新业务上线的目标、或者日常峰值的等比例目标、或者重大业务活动的预估支撑能力去设置每个API的目标能力（TPS是一步到位的按照吞吐能力设置的，推荐TPS模式，比如前面提到的添加购物车+购物车下单+付款这种流程就是一个漏斗模型，TPS设置为逐渐变小的模型即可），当然也可以在初期的测试中更谨慎一点，将目标量级设置得整体低一点，当最终能力达到之后建议可以调整原定目标量级到120%或者150%，验证限流准入/高可用基础设施的抗压能力。目标量级即当前压测场景中这个压测API的施压上限。而起步量级可以从5%或者10%开始，过程中视业务指标数据和被压测端的整体负载临时调整。

7、对服务器性能测试的看法？
针对服务器端的性能，以TPS为主来衡量系统的性能，并发用户数为辅来衡量系统的性能，如果必须要用并发用户数来衡量的话，需要一个前提，那就是交易在多长时间内完成，因为在系统负载不高的情况下，将思考时间(思考时间的值等于交易响应时间)加到串联链路（场景）中，并发用户数基本可以增加一倍，因此用并发用户数来衡量系统的性能没太大的意义。同样的，如果系统间的吞吐能力差别很大，那么同样的并发下TPS差距也会很大

8、系统的性能决定的要素？跟并发用户数的关系？
由TPS决定，跟并发用户数没有多大关系。
系统的最大TPS是一定的（在一个范围内），但并发用户数不一定，可以调整。
建议性能测试的时候，不要设置过长的思考时间，以最坏的情况下对服务器施压。