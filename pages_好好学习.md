- JVM
	- 用的Sun的HotSpot
	- 内存模型
		- 程序计数器
			- 用于记录分支循环线程切换
		- 堆
			- 线程公有
			- new出来的对象所属内存
			- 类，方法，变量，常量
			- OOM，内存溢出通常指堆内存溢出，调优也通常是调整堆内存
			- 分区
				- 新生代
					- 伊甸区、幸存0区、幸存1区
					- gc频繁，朝生夕死
				- 老年代
					- 大对象直接进入老年代
				- 永久代
					- 永久区不存在垃圾回收，存储类信息和Java运行时环境。永久代也被称为方法区或非堆
					- jdk1.6：永久代，常量池在永久代
					- 1.7：常量池在堆，不存在永久代
					- 1.8：无永久代，常量池在元空间
				- 堆内存大小调整参数
					- -Xms1024m：设置初始化堆内存
					- -xmx1024m：设置最大堆内存
					- -XX:+PrintGCDetails ：打印gc回收信息
					- -XX:+HeapDumpOnOutOfMemoryError：当堆内存溢出错误时生成内存快照
					- -XX:+MaxTenuringThreshold=99：调整新生代gc多少次进入老年代
				- 项目中出现过堆内存溢出错误，上传大文件时出现，通过扩大运行内存
				- 调优工具：jprofilter
					- 定位内存溢出位置
		- 栈
			- 虚拟机栈
				- 线程私有
				- 基本数据类型和引用所属内存
				- 实例方法
				- 会出现栈溢出错误
			- 本地方法栈
				- native修饰的方法，用于调用本地方法，即c或c++方法
		- 本地方法区
			- 线程公有
			- 存储final修饰的变量
			- 有常量池，字符串存储在该位置
			- static，类信息
		- 寄存器：离cpu更近，用于充当cpu和缓存的中间交换区
	- 类加载
		- 过程：加载，链接（验证，准备，解析），初始化
			- 加载：将字节码数据加载到内存，将数据转换为方法区内数据，并将其加载到堆作为方法区入口
			- 验证：确保加载的类信息符合jvm规范
			- 准备：为类变量分配内存并设置默认值
			- 解析：将符号引用替换为直接引用
			- 初始化：对类变量进行初始化。会先初始化父类。静态遍历>静态代码块
		- 类加载器
			- 应用程序加载器：类路径
			- 扩展类加载器：ext路径
			- 虚拟机加载器：lib路径
			- 启动类加载器
		- 双亲委派机制：
			- 先找父类能不能加载该类，如果可以则会优先使用父类的加载器加载该类，直到不能才会使用子类进行加载
			- 好处：
				- 使基础类库统一，比如Object,String
				- 避免多份相同字节码加载
	- 垃圾回收
		- 分类
			- 轻gc
			- 重gc
		- 新生代会不断gc，默认在gc 15次以后还没有死亡的对象进入老年代；大对象直接进入老年代
		- GC算法
			- 标记清除算法：gc之后进行标记，统一进行清除。内存碎片较多，不需要多余内存空间
			- 标记复制算法：进行内存分片，gc之后进行复制移动。对象存活率低使用该算法，也就是新生代。占用内存较多。
			- 标记压缩算法：
			- 分代收集算法
				- 年轻代：复制算法
				- 老年代：标记清除+标记压缩
		- 判断对象是否已死
			- 引用计数法：每多
			- 可达性分析法
		- 引用类型
			- 强
			- 弱
			- 软
			- 虚
	- 性能监控调优
	- 面试题目
		- 什么是OOM和栈溢出
		- JVM是什么
		- 类加载器有哪些，作用
		- JVM常用调优参数
		- 内存快照如何抓取，怎么分析DUMP文件
		- 什么是双亲委派机制
		- native
			- 用JNI调用本地库，c或c++的接口
	-
		- 标记清除算法
		- 标记复制算法
	-
		- 引用计数法
		- 可达性分析法
	-
	-
	-
- 计算机网络
	- OSI七层模型
		- 应用层
			- 控制应用
			- http，telnet，ssh，https，ftp
		- 表示层
			- 格式化数据
			- ASCLL,JEEPG,MP3
		- 会话层
			- 控制会话
			- PHP,JSP,SQL
		- 传输层
			- 建立端到端连接，进行数据传输
			- 有TCP,UDP
		- 网络层
			- 作用：IP寻址
			- 设备：路由器进行路由寻址
			- 单位：pdu
		- 数据链路层
			- 设备：交换机
			- 通过MAC地址转发数据，逻辑链路控制
		- 物理层
			- 单位bit
	- 协议
		- TCP/IP
			- 滑动窗口
			- 更安全
		- IP
			- 在互联网中标识某台主机地址的数字。网络层协议
		- UDP
			- 传输层协议
			- 不安全
			- 短连接
		- DNS
			- 用于解析域名为ip地址
		- HTTP
			- 概念
				- 无连接
				- 无状态
				- 超文本传输协议
				- 建立在TCP/IP之上的应用层协议
			- 请求
				- 请求行
					- 请求方法
						- GET,POST,PUT,DELETE,HEAD
					- URL
					- 协议版本
				- 请求头
					- 头部字段名
				- 请求体
					- 请求数据
				- 空行
			- 响应
				- 状态行
					- 响应码
					- 协议版本
				- 消息报头
					- 时间戳
					- 报文长度
					- 内容编码
					- 数据类型
						- text
						- image
				- 空行
				- 响应正文
		- HTTPS
			- 进行数据加密，安全的HTTP协议
		- WebSocket
			- 建立在http协议之上的建立长连接的协议
			- wsc
		- FTP
			- 传输文件协议
		- SMTP
			- 邮件传输协议
	- 面试题
		- 浏览器输入网址后的过程
			- 进行dns解析，将域名解析为ip地址
		- tcp三次握手四次挥手过程，为什么时三次握手，四次挥手
			- 建立连接过程
				- 客户端包装序列号发送到服务端
				- 服务端向客户端发确认码和序列号
				- 客户端向服务端发送确认码
			- 断开连接过程
				- 客户端向服务端发送断开请求，服务端接收请求并确认
				- 服务端向客户端发送断开请求，客户端接收请求并确认
			- 为什么三次握手
				- 既能保证效率又能保证数据可靠
			- 为什么四次挥手
				- 全双工，需要保证两边都断开连接
		- tcp和udp区别
			- tcp有连接且可靠 ，udp无连接，不可靠
			- tcp需要握手和挥手建立断开连接，udp不需要
			- tcp基于字节流，udp基于报文
		- http状态码，请求信息，响应信息
			- 请求类型
				- GET
				- POST
				- PUT
				- DELETE
				- Get和Post的区别
- 数据结构算法
	- 概念
		- 概念：研究数据存储方式，存储复杂数据关系的数据有助于后期再利用
			- 逻辑结构：指数据之间一对一，一对多，多对多的数据关系
			- 物理结构：数据在磁盘上的存储结构，指数据在磁盘上是集中存放还是分散存放。选择顺序表或链表。
		- 如何衡量算法好坏
			- 健壮性，准确性
			- 时间复杂度：程序耗时。O(频度)表示。
			- 空间复杂度：在内存中建立的对象的大小和代码占用内存的和。
	- 线性表
		- 概念：线性表存储一对一数据关系的数据。
		- 顺序表：物理地址连续，对应数组。维护索引，查询快，增删改慢。空间利用率高，但必须初始化时确定大小。查询特定元素，时间复杂度为O(1)。
		- 链表：物理地址不联系，靠头尾指针记录数据关系。查询慢，增删改只需要移动指针。空间利用率较低，但可以使用不连续的内存，也可以不知道需要开辟的内存的大小。
			- 单链表翻转
			- 两个有序链表合并
	- 队列：先进先出，对应Queue
	- 栈：先进后出，对应Stack
	- 字符串：
		- Java中底层是char数组
	- 树
		- 概念
			- 度
			- 层
			- 结点
			- 有序数无序树
			- 森林
		- 分类
			- 二叉树
			- 完全二叉树：除最后一层结点外为满二叉树，且最后一层结点从左到右分布
			- 满二叉树：除叶子结点外其他结点的度都是2
			- 二叉排序树
		- 遍历
			- 前序
			- 中序
			- 后序
			- 层序
	- 图
		- dfs
		- bfs
	- 哈希表
	- 算法
		- 排序算法
			- 冒泡
			- 选择
			- 快排3
		- 查找
			- 二分查找
- Docker
	- 应用场景
		- 持续化集成
		- 微服务架构
		- 提供弹性云服务，方便动态扩容和缩容
	- 背景：开发测试运维出现各种环境问题，使用虚拟机可以直接把环境复制过去，解决环境不同导致的问题。
	- 虚拟机和linux容器的区别：
		- 虚拟机抽象完整的操作系统，包括硬件资源，占用资源多，启动慢
		- docker是进程隔离，启动快，占用资源少
	- docker是什么：docker是linux容器的封装，并提供简单接口，可以像操作代码一样对容器进行创建，分享，编辑。
	- 仓库
		- docker hub，存放docker镜像的远程库
		- 命令
			- docker pull mysql
			- docker login
			- docker logout
			- docker tag
			- docker push
	- 容器
		- image生成的容器实例，称为容器文件
		- 命令
			- docker run -it mysql /bin/bash
				- -v
				- -p
			- docker ps -a
			- docker ps
			- docker stop
			- docker start
			- docker rm
			- docker restart
			- docker exec -it   /bin/bash
			- docker export 容器id > hello.tar 导出容器快照
			- docker import 容器 id 导入容器快照
	- 镜像
		- 将应用程序和依赖打包成镜像，通过镜像文件生成多个运行容器。可以在image容器基础上进行加工，生成自己的image镜像
		- 命令
			- docker search
			- docker images
			- docker rmi
			- 创建镜像
				- docker build -t 镜像名 .
				- 写DockerFile文件
			- docker tag 为镜像加标签
			-
	-
- Nginx
	- 三个模块
		- 全局块：配置工作进程数、并发数
		- events块：配置最大连接数，
		- http块：嵌入多个server块，配置文件压缩
			- server块
				- listen
				- server_name
				- location
					- 通配符
						- =
						- /
						- ^~
						- ~*
					- root
					- index
	- 使用场景
		- 负载均衡http块
			- 轮询 `upstream web_servers {  server localhost:8081; server localhost:8082;  } `
			- 权重 `upstream test { server localhost:8081 weight=1; server localhost:8082 weight=3;  server localhost:8083 weight=4 backup;}`
			- ip_hash `upstream test { ip_hash;server localhost:8080;server localhost:8081;}`
				- 可用于解决分布式session问题
			- fair：按服务器响应时间进行分配请求
			- url_hash：使每个url每次都定位到一个服务器，有缓存时可提升性能
		- 反向代理
			- proxy_pass
			- 代理服务器接收到请求后，将其转发给内部网络的服务器
		- Http服务器
		- 静态文件服务器
		- 动静分离
			- 静态文件进行指定
			- 服务进行反向代理
	- 面试题
		- 正向代理和反向代理的区别
			- 反向代理是对服务进行转发，只对外暴露代理服务器，用来隐藏提供服务的服务器
			- 正向代理是代理客户端去对服务器进行请求，如svn代理访问服务
		- 负载均衡类型
			- 轮询，加权，ip_hash，url_hash，fair
		- 如何开启压缩
			- 将配置放到http块，响应头编码类型变成gzip
		- nginx优点，什么是nginx？
			- 免费，跨平台，非阻塞，高并发，内存消耗小
			- nginx是一个web，反向代理服务器
		- 如何处理Http请求
			- 在Nginx启动时，先解析配置文件，监听端口和ip，请求响应后fork子进程进行进行连接。
		-
- 设计模式
	- 六大原则
		- 里氏替换原则：子类可以替换任意父类
		- 最少知道原则：一个实体应该尽可能少与其他接口有关联
		- 合成复用原则：尽量使用组合而不是继承
		- 开闭原则：新增功能时，新增接口，不要修改原有接口
		- 接口隔离原则：降低接口之间的耦合度，使用多个接口，功能
		- 依赖倒转原则：面向接口编程而不是实现类
	- 二十三种设计模式
		- 创建型
			- 单例
				- 懒汉
				- 饿汉
				- 线程安全
				- 双检验
			- 工厂模式：创建复杂对象，屏蔽对象具体构造方式
			- 抽象工厂模式：先创建工厂，在用工厂创建对象。适用于产品工厂
			- 建造者：多个基础组件构成，适用于组合灵活，组件不变的情况
			- 原型模式：适合创造重复对象，利用clone方法生成重复对象，提高性能
		- 结构型
			- 适配器模式：使不兼容的接口一起工作，调用a接口方法时可以使用到b接口的方法
			- 桥接模式：将抽象部分与实现部分分离，使其都可以独立变化。传入实例对象
			- 过滤器模式：使用不同模式过滤一组对象
			- 组合模式：就是合成复用
			- 装饰器模式：在不改变原有类结构的同时，对其添加新功能
			- 代理模式：为其他对象提供代理控制这个对象的访问
		- 行为型
			- 策略模式：用于不同算法的抽象，可以搭配工厂模式减少if else
			- 模板模式：使用抽象类，提取抽象通用算法，封装不变的部分，方便扩展
			- 观察者模式：监听器
			- 责任链模式：拦截器，js事件冒泡，过滤器
			- 状态模式：行为随状态改变而改变的场景
			- 空对象模式：用于处理对象为空时提供默认值
			- 访问者模式：将数据结构与数据操作分离
			- 备忘录模式：保存一个对象的某个状态，以便在适当的时候恢复对象
	- J2EE设计模式
		- mvc
	- Spring中使用的实际模式
		- 工厂模式：BeanFactory
		- 单例模式：每个bean都是单例的
		- 模板模式：RedisTemplete
		- 代理模式：aop，Cglib动态代理
	- jdk使用的设计模式
		- 建造者：StringBuilder
		- 责任链：servlet中的过滤器
		- 观察者：Swing的监听方法
		- 单例模式：
		- 代理模式：jdk动态代理
- Redis
	- 五大数据类型
		- String
		- List
		- Set
		- ZSet
		- hashMap
	- 持久化策略
		- RDB
			- 可设置持久化机制，如100s更新10次，快照数据到.rdb文件。默认rdb
			- 优点：性能差，恢复快
			- 缺点：易丢数据，如最后一次触发持久化数据时宕机，会丢失本次全部数据
		- AOF
			- 记录所有写指令
			- 优点：性能好，更安全
			- 缺点：恢复缓慢
	- springboot集成
		- redis starter
		- redisTemplate
	- 缓存雪崩，缓存穿透，如何避免
		- 缓存雪崩
			- 大量缓存在同一时间失效，这样失效时，会给后端服务造成极大压力，导致服务器崩溃
			- 解决方案：
				- 对key设置不同的过期时间，让缓存失效的时间尽量均匀
		- 缓存穿透
			- 大量请求查询某个不存在的key，对后端数据库造成很大压力，叫做缓存穿透
			- 解决方案：
				- 对查询结果为空的情况也进行缓存
				- 对一定不存在的key进行过滤
	- 集群，哨兵机制
	- 优点，使用场景
		- 用作分布式缓存
		- 计数器
		- 消息队列
		- 排行榜
		- 双向链表
	- 项目使用
		- 使用redis缓存了传感器实时数据，实时数据需要频繁读取，引入缓存极大降低了数据库压力，提升了服务器性能。
		- 使用redis缓存字典数据，token和用户信息。
	- 面试题
		- redis有哪些数据类型？
			- String，List，Set，ZSet，Hash
		- redis有哪些持久化方式？
			- rdb
			- aof
			- 两个都配置了，优先加载aof
		- redis是什么？
			- kv内存数据库
			- 多种数据结构
			- 支持事物
			- 支持异步持久化
		- redis比起memcached有哪些优势？
			- 数据类型更丰富
			- 可以持久化
			- 支持事物
			- redis速度更快
		- redis数据淘汰策略
			- 5种，当内存达到限制，且仍然在执行写入指令时发生
			- allkeys-lru：尝试回收使用最少的键
			- volatile-lru：从过期集合中回收使用最少的键
			- allkeys-random：从所有集合中随机回收键
			- volatile-random：从过期集合中随机回收键
			- volatile-ttl：从过期集合中回收存活时间最短的键
		- redis一个字符串类型的值能存储多达容量
			- 512M
		- redis支持的ava客户端有哪些？
			- jedis
		- redis如何设置过期时间？如何进行持久化？
			- expire  persist
		- redis如何设置用户名密码
			- config set
		- 如何选择合适的持久化机制
		- 哪些办法可以降低redis的内存使用情况
			- 使用合适的数据结构。如hash占用内存较小
		- redis如何做主从，哨兵，主从不一致解决
			- 通过配置一个主节点，多个从节点。
			- 哨兵机制
			- 主从不一致
				- 业务实时性不高，忽略
				- 强制读主库
		- 修改配置不重启redis会生效吗
			- 用命令修改的方式可以生效
		- redis各数据类型的使用场景
			- list双向链表
			- set
		- 缓存一致性解决（保证最终一致性）
			- 给缓存设置过期时间
			- 先删除缓存，更新数据库，再删除缓存
		- 性能优化方案
		- redis如何做异步队列，延时队列
		- redis使用什么协议
			- redis使用RESP协议，该协议是redis客户端和服务端之间使用的通讯协议
			- RESP的特点：实现简单，快速解析，可读性好
		- redis做发布订阅
			- 一个客户端subscribe chat
			- 另一个客户端publish chat
		- 主从如何实现？
			- 主节点将内存快照后，把数据发给从节点，从节点将数据恢复到内存。之后主节点每次新增数据后，会以二进制文件的方式，将语句发送给从节点，从节点执行。
		-
		-
- RabbitMQ
	- 什么是消息队列？
		- 存储消息的数据结构。生产者只发送消息，消费者只接收消息
	- 为什么使用消息队列
		- 解耦
			- bcde四个模块需要a的数据，如果不用中间件，就需要a系统写四份冗余代码。用中间件可以让bcde都直接取a存到中间件的数据
		- 削峰
			- 如某时刻请求过多，系统处理不过来，容易导致mysql崩溃。可以先全部放到mq，定时拉取请求，防止mysql崩溃
		- 异步
			- 如发短信，发邮件，可以降低响应时间。对于非必要的业务可以使用
	- 优点
		- 可靠性
		- 多协议
		- 多客户端
		- 支持集群
		- 丰富的消息分发机制
	- helloWorld
		- 导入starter
		- 写配置类（队列，交换机，路由）
		- 写生产者
		- 写消费者
		- bean生命周期，继承BeanPostProcessor，实现postProcessAfterInitialization方法
	- 组成
		- 队列：存储消息
		- 交换机：用来按照一定路由规则转发消息到不同队列
		- 路由：
		- 生产者：将消息发到队列
		- 消费者：监听队列，接收队列消息
	- 交换机类型
		- 直连：一对一。需要交换机和队列使用路由绑定。
		- 主题：路由键支持通配符。两种通配符，通配符前面必须加.
			- “ * ”：只匹配一个词，a.*可以匹配a.b,a.c但不能匹配a.b.c
			- "#"：匹配多个词
			- 会根据通配符路由转发到不同队列
		- 广播：一个发送到交换机的消息都会被转发到与该交换机绑定的所有队列上。没有路由。形成发布订阅效果。直接向交换机发送消息，与该交换机绑定的所有路由都可以收到消息。
		- headers exchange
	- 事务
	- 协议
		- AMQP协议
	- 确认机制
	- 死信队列
	- 延迟队列
	- 高可用
		- 生产者如何将消息可靠的投送到MQ
		- MQ如何可靠的将消息投送到消费者
- MySQL
	- 架构模式
		- 会话层：与客户端建立连接
		- 存储引擎层：用来存储数据
		- 服务层：缓存，sql解析器，sql接口，查询优化器
	- 存储引擎
		- innodb：支持事务
		- myisiam：不支持事务
	- 锁分类
		- 表锁：ddl操作都会上表锁，表锁并发度低，触发表锁会锁住该表所有数据，直到当前事务修改完成后，才会释放锁。
		- 行锁：并发度高，性能好。for update
		- 读锁：事务上该锁后，其他事务只能读不能修改
		- 写锁：事务上写锁后，其他事务不能在对其上锁，既不能读取也不能修改
	- 事务特性
		- 原子性：一个操作，要成功都成功，要失败都失败
		- 持久性：事务执行完成，会持久化到数据库
		- 隔离性：不同事务之间不会互相影响，允许多个事务同时访问数据库
		- 一致性：事务开始前和事务结束以后，数据库完整性不被破坏
	- 隔离级别
		- 未提交读：脏读。
		- 提交读：不可重读
		- 可重复读：幻读
		- 可串行化：
	- mvcc：多版本并发控制
		- 通过隐藏字段实现。每行记录维护事务版本，一个事务对记录的修改删除操作会让记录的版本号加1，如果其他事务修改该记录时，查看到版本号比开始的版本号大，那么放弃本次操作。
	- 索引：
		- 索引是一种数据结构，用来快速查询数据
		- 类型：
			- B+树索引
			- Hash索引
			- 全文索引
	- 数据结构
		- 二叉查找树：排序的二叉树，时间复杂度log2n
		- 平衡二叉树：防止出现树变链表的情况，进行节点调整
		- B树：海量数据下，二叉树层高太高，所以使用每个结点存储多个键值
		- B+树：
			- 类似B+树，不过只有叶子节点存储数据，这样每个节点可以存储更多键，页的默认大小是16kb，一般三层树就可以存储千万数据
			- 页子节点：排序存储所有数据
	- 乐观锁，悲观锁
		- 乐观锁：性能好。
			- 版本号机制：不上锁，通过版本号机制，数据库行维护一个版本号，在被修改时判断版本号是否和上次相同，如果版本号不同，取消修改。
			- cas：比较并替换。
		- 悲观锁：性能差，并发度低。每次修改都上互斥锁，其他事务无法得到该锁，对其进行修改。
	- 数据类型
		- int，bigint
		- double，float，decimal
		- char，varchar
		- text
	- 查询优化
		- 索引
			- 本质是数据结构
		- 索引类型
			- 聚簇索引：主键索引，b+树，页子节点存储数据
			- 非聚簇索引：非主键索引，叶子节点存储主键索引，需要进行回表
			- 唯一索引
			- 普通索引
			- 主键索引
			- 组合索引
				- 最左匹配原则
		- explain分析
			- type
				- all
				- index
				- range
				- ref
				- eq_ref
			- key
			- rows
	- 三大范式
		- 第一范式：不存在表中有表的情况
		- 第二范式：解决部分依赖，即非主键列没有全部依赖主键列
		- 第三范式：解决传递依赖，即非主键列既依赖主键列，也以来某非主键列
	- 适当字段冗余
	- 候选键，主键，外键
		- 候选键：不可重复的键
		- 主键；特殊候选键，一张表只能有一个主键，且必须只有一个
		- 外键：做外键约束，维持数据完整性
	- sql关键字
		- select
		- where
		- having
		- group by
		- order by
		- limit
		- as
		- disctinct
		- union
	- 聚合函数
		- min
		- max
		- sum
		- count
	- 面试题
		- 如何优化查询
			- explain分析查询语句
			- 查询不要差全部字段，要什么查什么。降低io
			- 建立合适索引
		- innodb和myisiam区别
		- 项目中的优化场景
			- 不要在for循环中进行sql操作
			- 不要select *
			- 查询条件的字段不能用模糊，不能使用函数，不能计算
		- 哪些字段建立索引？
			- 数据散列度高
			- 小字段，如text不适合建立索引
		- 索引缺点
			- 大量占据磁盘空间
- 网络编程
	- Socket：服务器监听端口，客户端和服务器建立连接通道，通过io发送数据到服务器
	- WebSocket
		- springboot集成
			- 导入starter
			- 使用相关注解
		- 概念
			- 建立在tcp协议之上的协议，可以服务端主动向客户端发起请求，握手时使用http协议
		- 使用场景
			- 聊天室，之前都是客户端轮询实现。可以通过服务器主动推送实现。
		- api
			- 构造实例
			- 发送消息
			- 收到消息回调
			- 打开连接回调
			- 连接失败回调
			-
- Java基础
	- 基础语法
	- 数据类型
	- 面向对象
		- 什么是面向对象，与面向过程的区别
		- 抽象，多态，继承
	- 异常处理
		- 作用
		- try，catch，finally
	- 泛型
		- 作用
	- 反射
		- 作用
	- 注解
	- IO
	- 集合
	- String
	- Object
	- 枚举
	- 并发
	- JUC
	- 面试题
		- 如何理解面向对象，和面向过程的区别
		- 数据类型，装箱拆箱
		-
		-
- 工具
	- Maven
		- maven是什么
		- maven依赖范围
		- maven依赖冲突怎么解决
		- 多模块聚合
		- dependencies和dependencyManagement区别
		- maven生命周期
	- Git
		- git是什么
		- git常用命令
		- git合并分支
		- git回滚
		- git使用流程
	- 持续集成
		- jenkins+gitlab+docker+maven持续化集成部署服务
			- jenkins安装gitlab hook+maven+docker
- Linux
	- 文件操作
		- mkdir
		- touch
		- cat
		- tac
		- vim
		- rm
		- rm -rf
		- mv
		- cp
		- ls
		- cd
		-
	- 用户权限
		- chomd
		- chown
		- chgrp
	- 进程
		- ps -ef
		- top
	- 查找
		- find
		- grep
- Spring全家桶
	- Spring MVC
	- MyBatis
	- MyBatis-plus
	- Spring
	- Spring Boot
	- Spring Cloud
	- Spring Cloud Alibaba
- 项目
	- 隧道项目
		- 亮点
			- 接口幂等
			- aop打印日志
			- 查询优化
			- socket编程
			- redis缓存实时数据
			- rabbitmq异步发短信
	- util监控项目
		- 亮点
			- 多数据源
			- 多redis数据源
			- 策略模式，根据不同算法发送不同的短信
			- 异常统一处理
	- 警察列管项目
		- 亮点
			- 反射，注解，泛型实现分值计算统一算法
- 面试准备
	- 简历
	- 自我介绍
	- 项目介绍
		- 智慧隧道
		- 公安e管
	- 离职原因
	- 公司了解
	- 谈薪