# JVM

![1569773371671](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1569773371671.png)

## JVM体系结构概览

![1573560851646](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573560851646.png)

### 类加载器

![1573539501440](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573539501440.png)

![1573540653088](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573540653088.png)

#### 双亲委派机制

![1573541329190](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573541329190.png)

#### 沙箱安全

##### 什么是沙箱？

 Java安全模型的核心就是Java沙箱（sandbox），什么是沙箱？沙箱是一个限制程序运行的环境。**沙箱机制就是将 Java 代码限定在虚拟机(JVM)特定的运行范围中，并且严格限制代码对本地系统资源访问，**通过这样的措施来保证对代码的有效隔离，防止对本地系统造成破坏。沙箱主要限制系统资源访问，那系统资源包括什么？——CPU、内存、文件系统、网络。不同级别的沙箱对这些资源访问的限制也可以不一样。

 所有的Java程序运行都可以指定沙箱，可以定制安全策略。

Java沙箱由以下部分组成：

- 类加载器结构（例如命名空间）
- class文件校验器
- 内置于Java虚拟机（和Java语言）的安全特性（例如对指针操作的屏蔽等）
- Java安全管理器（Java Security Manager）和Java API组成

前三个基本都是**内置**实现在JVM和Java语言中的，只有Java安全管理器（Java Security Manager）是能被开发者控制的，用来保护系统不被JVM中恶意的代码破坏的。这样，**绕过java沙箱其实就转化成绕过java security manager**。

**Java Security Manager的一个典型应用场景是jvm需要加载运行一段代码，但是这段代码是不可信的，例如来自用户的输入、上传、反序列化指定的bytecode或者来自网络远程加载，这种情况下，需要防止不可信来源的恶意代码对系统造成破坏。其实这就是沙箱的应用场景。**



![image-20191218211211241](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\image-20191218211211241.png)

##### 沙箱绕过

https://www.anquanke.com/post/id/151398#h2-1

### 执行引擎

负责解释命令，提交操作系统执行

### PC 寄存器   Program Counter Register

![1573559157878](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573559157878.png)

### 小总结

![1573559737059](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573559737059.png)

### 方法区

![1573559899713](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573559899713.png)

![1573560961658](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573560961658.png)

### java栈  heap堆

栈管运行，堆管存储

![1573561033811](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573561033811.png)

![1573561610136](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573561610136.png)

![1573561393393](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573561393393.png)

![1573561987229](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573561987229.png)

java 方法 == 栈帧

**Exception in thread "main" java.lang.StackOverflowError**

**由于方法的加载，深度的调用撑爆栈导致****，**是一个错误****

### 堆+栈+方法区的交互关系

![1573562352776](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573562352776.png)

### 堆 heap

![1573562935140](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573562935140.png)

java 8 为元空间。      物理上为两部分：新生+养老

![1573563502766](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573563502766.png)

#### 对象生命周期和GC

 ![1573701040841](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573701040841.png)

#### 元空间

![1573701406296](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573701406296.png)

![1573701430536](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573701430536.png)

## 堆参数调优

![1573701741401](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573701741401.png)

![1573701774061](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573701774061.png)

**java堆一般占物理内存的1/4**

![1573702063978](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573702063978.png)

![1573717293309](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573717293309.png)

![1573718499432](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573718499432.png)

### GC详细日志收集

![1573716902259](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573716902259.png)

![1573722572587](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573722572587.png)

## GC（分代收集算法）Generational collection algorithm

![1573719816153](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573719816153.png)

![1573719858526](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573719858526.png)

![1573720925726](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573720925726.png)

### GC四大算法

#### 引用计数法----了解即可  不会用

![1573721173205](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573721173205.png)

#### 复制算法（Coping)

![1573721600728](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573721600728.png)

![1573721794774](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573721794774.png)

![1573722051057](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573722051057.png)

![1573722265822](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573722265822.png)

![1573722406460](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573722406460.png)

#### 标记清除（Mark-Sweep)

![1573723767384](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573723767384.png)

![1573723902798](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573723902798.png)

![1573723932409](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573723932409.png)

![1573724050257](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573724050257.png)

#### 标记压缩（Mark-Compact)

![1573724226615](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573724226615.png)

![1573724290838](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573724290838.png)

![1573724311876](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573724311876.png)

#### 总结

![1573724500376](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573724500376.png)

![1573724551079](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573724551079.png)

![1573724632780](C:\Users\Min\AppData\Roaming\Typora\typora-user-images\1573724632780.png)

