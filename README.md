如下是C++后台研发技术路线以及知识点，这里有很多细节，还需要不断完善。 

欢迎大家[提交PR](https://www.programmercarl.com/qita/join.html)来一起完善这个知识库，成为contributor！ 

👉 如果你是编程零基础，或者想入门C++，推荐 [卡码网C++基础课](https://kamacoder.com/course.php?course_id=1)

# C++primer B站视频讲解 

* [学习C++书籍推荐](https://www.bilibili.com/video/BV1rK4y1e7ed)
* [听说C++ primer 太厚了 看不进去？](https://www.bilibili.com/video/BV1Z5411874t)
* [C++ primer 第一章，你要知道的知识点还有这些！](https://www.bilibili.com/video/BV1Kv41117Ya)
* [C++ primer 第二章，前两节](https://www.bilibili.com/video/BV1MA411j74g)

（玩命更新ing...）

# 编程语言C++

* [C++primer5笔记代码资料](https://github.com/youngyangyang04/TechCPP/tree/master/docs/C++primer5笔记代码资料)
* [volatile static const extern等关键字](./problems/volatile,static,const,extern等关键字.md) 
* [宏定义和展开、内联函数区别](./problems/宏定义和展开、内联函数区别.md)
* 常用库函数实现
    * [malloc,strcpy,strcmp的实现，常用库函数实现，哪些库函数属于高危函数](./problems/malloc,strcpy,strcmp的实现，常用库函数实现，哪些库函数属于高危函数.md)
* [STL原理及实现](./problems/STL原理及实现.md)
* [虚函数的作用和实现原理，什么是虚函数,有什么作用?](./problems/虚函数的作用和实现原理，什么是虚函数,有什么作用.md)
    * [纯虚函数，为什么需要纯虚函数？](./problems/纯虚函数，为什么需要纯虚函数.md)
    * [为什么需要虚析构函数,什么时候不需要?](./problems/为什么需要虚析构函数,什么时候不需要.md)
    * [内联函数、构造函数、静态成员函数可以是虚函数吗?](./problems/内联函数、构造函数、静态成员函数可以是虚函数吗.md)
    * [构造函数中可以调用虚函数吗?](./problems/构造函数中可以调用虚函数吗.md)
    * [为什么需要虚继承?虚继承实现原理解析](./problems/为什么需要虚继承.md)

* [C++ 内存分配机制](./problems/C++内存分配.md)
* 指针
    * [迭代器与普通指针有什么区别](./problems/迭代器与普通指针有什么区别.md) 
    * [C++的智能指针及其原理](./problems/C++的智能指针及其原理.md)
* [override和overload的区别](./problems/override和overload的区别有那些.md)
* [写string类的构造，析构，拷贝函数](./problems/写string类的构造，析构，拷贝函数.md)

# 数据结构与算法

* [数据结构与算法学习攻略](https://github.com/youngyangyang04/leetcode-master)

# 设计模式

* [C++设计模式](https://github.com/youngyangyang04/DesignPattern)
* [C++单例模式](./problems/C++单例模式.md) 
* [用C++设计一个不能被继承的类](./problems/用C++设计一个不能被继承的类.md)
* [如何定义一个只能在堆上定义对象的类?栈上呢](./problems/如何定义一个只能在堆上定义对象的类栈上呢.md)
* 重类构造和析构的顺序

# 操作系统 

* linux的内存管理机制，内存寻址方式，什么叫虚拟内存，内存调页算法，任务调度算法 
* [锁：互斥锁，乐观锁，悲观锁](./problems/锁：互斥锁，乐观锁，悲观锁.md) 
    * [死锁必要条件及避免算法](./problems/死锁必要条件及避免算法.md) 
* 动态链接和静态链接的区别
* 常见的信号、系统如何将一个信号通知到进程
* linux系统的各类同步机制、linux系统的各类异步机制
* 如何实现守护进程
* 标准库函数和系统调用的区别

# linux 服务器
* 32位系统一个进程最多有多少堆内存
* 五种I/O 模式:阻塞I/O,非阻塞 I/O,I/O 多路复用,信号驱动 I/O,异步 I/O
    * select 模型和 poll 模型，epoll模型
    * socket服务端的实现，select和epoll的区别(必问)
    * epoll哪些触发模式，有啥区别？
* 用户态和内核态的区别
* linux文件系统：inode，inode存储了哪些东西，目录名，文件名存在哪里

# 计算机网络

* TCP和UDP区别
* TCP和UDP头部字节定义 
* TCP和UDP三次握手和四次挥手状态及消息类型 
* time_wait，close_wait状态产生原因，keepalive
* 什么是滑动窗口，超时重传
* 列举你所知道的tcp选项
* connect会阻塞检测及防止，socket什么情况下可读？ 
* socket什么情况下可读？
* connect会阻塞，怎么解决?(必考必问) 
* keepalive是什么？如何使用？
* 长连接和短连接 
* UDP中使用connect的好处 
* DNS和HTTP协议，HTTP请求方式 

# 数据库 

* 谈谈数据库中索引的理解，索引和主键区别
* 现在普通关系数据库用得数据结构是什么类型的数据结构 
* 索引的优点和缺点
* 系型数据库和非关系数据库的特点 
* 乐观锁与悲观锁的区别 
* 数据库范式:第一第二第三范式
* 数据库日志类型作用 
* B TREE 和B+TREE的区别 
* union和join 

# 海量数据处理 

* bitmap 
* Map-Reduce原理 
* BloomFilter原理 
* Trie树原理 
* LSM树原理 

# linux下操作命令以及工具

* [工作中常用的linux 命令](./docs/linux常用操作命令.md)
* 编译工具GCC 
* 调试工具GDB
* 性能优化工具Perf 
* 内存泄露检查工具Valgrind
* makefile编写

# 程序员求职

* [简历模板](https://github.com/youngyangyang04/Markdown-Resume-Template)


# 程序员的工具

工欲善其事必先利其器

* [vim配置](https://github.com/youngyangyang04/PowerVim)


# 适合新手的开源项目

* [联机五子棋（c实现）](https://github.com/youngyangyang04/Gomoku)
* [fileHttpServer(go语言实现)](https://github.com/youngyangyang04/fileHttpServer)
* [Sqlgen（shell脚本实现的批量操作mysql）](https://github.com/youngyangyang04/PowerSqlgen)
* [单机存储引擎（C++实现的跳表）](https://github.com/youngyangyang04/Skiplist-CPP)
* [NosqlAttack （python实现）](https://github.com/youngyangyang04/NoSQLAttack)

# 关于作者

大家好，我是程序员Carl，[《代码随想录》](https://programmercarl.com/other/publish.html)作者，哈工大师兄，先后在腾讯和百度从事分布式技术研发。

* [代码随想录网站](https://programmercarl.com)
* [代码随想录Github](https://github.com/youngyangyang04/leetcode-master)
* [代码随想录算法公开课](https://www.bilibili.com/video/BV1fA4y1o715)
* [卡码网-专业ACM练习网站](https://kamacoder.com/)



