1. 了解历史

2. 内存结构

3. 垃圾回收机制

4. 性能监控工具

5. 性能调优案例实战

6. 认识类的文件结构

7. 类加载机制

8. 字节码执行引擎

9. 虚拟机编译及运行时优化

10. Java线程高级

 

内存溢出问题的分析与解决：

VM arguments

–XX:+heapDumpOnOutOfMemoryError

-Xmm20m –Xmm20m

生成快照，工具定位问题

 

Jvm 可视化工具 在jdk /bin下jconsole

 

HotSpot VM(sun)、J9(IBM Technology for Java virtual Machine)、Microsoft、TaobaoVM等公司虚拟机

 

Java虚拟机内存管理

![img](file:///C:\Users\km\AppData\Local\Temp\ksohtml6864\wps1.jpg) 

 

***\*Java堆\****

存放对象实例

垃圾收集器管理的主要区域

新生代、老年代、Eden空间

OutOfMemory

-Xmx –Xms

 

***\*方法区\****

存储虚拟机加载的类信息、常量、静态变量，即编译器编译后的代码等数据（接口、方法、字段）

方法区和永久代

垃圾回收在方法区的行为

异常定义

 

运行时常量池、直接内存（nio）

 

***\*对象的创建\****

![img](file:///C:\Users\km\AppData\Local\Temp\ksohtml6864\wps2.jpg) 

 

***\*对象的结构\****

1. Header(对象头)，

   a) 自身运行时数据

i. 哈希值 GC分代

​	b) 类型指针

2. InstanceData

3. padding

 

***\*垃圾回收\****

如何判定对象为垃圾对象

引用技术法

可达性分析法

如何回收

回收策略

标记-清除算法（效率，空间问题）

复制算法

标记-整理算法

分代收集算法（根据新生代、老年代请求选择以上算法）

垃圾回收器

​	Serial（最基本，发展最悠久，单线程，主要在客户端）

​	Parnew(多线程)

​	Paraller（多线程，可控制的吞吐量）

​	Cms	

​	G1

何时回收

引用计数法：在对象中添加一个引用计数器，当有地方引用这个对象时，引用计数器的值+1，当引用失效时，计数器的值-1（不采用，对象相互引用无法GC）

 

可达性分析法：

作为GCRoots的对象，向下找

虚拟机栈

 方法区的类属性所引用的对象

 方法区中的常量所引用的对象

 本地方法栈中引用的对象

 

***\*复制算法：\****

堆

 新生代

 Eden 伊甸园

 Survivor 存活区(Form,To)

 Tenured Gen

 老年代

方法区

***\*CMS收集器Concurrent Mark Sweep\****

工作过程

​	初始标记

​	并发标记

​	重新标记

​	并发清理

优点：并发收集、低停顿

缺点：占用大量cpu资源、无法处理浮动垃圾、出现Concurrent Mode Failure、空间碎片

 

***\*G1收集器\****

 历史

 优势：并行与并发、分代收集、空间整合、可预测的停顿

 步骤：初始标记、并发标记、最终标记、筛选回收

 与cms比较

 

***\*内存分配策略\****

l 优先分配到Eden

l 大对象直接分配到老年代

l 长期存活的对象分配到老年代

l 空间分配担保

l 动态对象年龄判断

 

***\*J\*******\*ava IO/NIO\****

阻塞IO模型：最传统的一种IO模型，即在读写数据过程中会发生阻塞现象。当用户线程发出IO请求之后，内核会查看数据是否就绪，若未就绪就会等待数据就绪，而用户线程就会处于阻塞状态。

非阻塞IO模型：用户线程发起一个read操作后，并不需要等待，马上就等到结果。如果结果时error时，就知道数据没准备好，再次发送read操作。

多路复用IO模型：有一个线程不断轮询多个socket的状态，只有当socket真正有读写事件时，才真正调用实际的IO读写操作。

信号驱动IO模型：在信号驱动IO模型中，当用户线程发起一个IO请求操作，会给对应的socket注册一个信号函 数，然后用户线程会继续执行，当内核数据就绪时会发送一个信号给用户线程，用户线程接收到 信号之后，便在信号函数中调用IO读写操作来进行实际的IO请求操作。

异步IO模型：，只需要先发起一个请求，当接收内核返回的成功信号时表示IO操作已经完成，可以直接 去使用数据了。

J***\*avaio包\****

字节流（InputStream、OutputStream）和字符流(Reader、Writer)

***\*JVM类加载机制\****

分为五部分：加载，验证，准备，解析，初始化。

JVM提供3种类加载器：

启动类加载器（Bootstrap ClassLoader）、扩展类加载器（Extension ClassLoader）、应用程序类加载器（Application ClassLoader）

JVM通过双亲委派模型进行类的加载，自定义的类加载器要继承java.lang.ClassLoader

 

***\*双亲委派\****

当一个类收到了类加载请求，他首先不会尝试自己去加载这个类，而是把这个请求委派给父 类去完成，每一个层次类加载器都是如此，因此所有的加载请求都应该传送到启动类加载其中， 只有当父类加载器反馈自己无法完成这个请求的时候（在它的加载路径下没有找到所需加载的 Class），子类加载器才会尝试自己去加载。

目的：保证了使用不同的类加载器最终得到的都是同一个Object对象

![img](file:///C:\Users\km\AppData\Local\Temp\ksohtml6864\wps3.jpg) 

 

 

 

 

 

 

 

 

 

 

 

 