### 只在栈上创建对象

要使得对象只能在栈上创建，可以将类的new操作符设置为private或者delete。这样一来，由于在堆上创建对象需要调用new操作符，这个类的对象就只能在栈上创建了。例如：

```
class StackOnly {
private:
    static void* operator new(size_t size) = delete;
    static void* operator new[](size_t size) = delete;
    
public:
    StackOnly() {}
    ~StackOnly() {}
};
```

### 只在堆上创建对象

要使得对象只能在堆上创建，可以将类的析构函数设置为private，并提供一个public的函数来删除对象。这样一来，由于在栈上创建对象需要在作用域结束时调用析构函数，这个类的对象就只能在堆上创建了。

但是这样会导致一个问题，就是当我们创建对象后忘记手动删除，就会引发内存泄漏。因此，可以将删除函数封装在智能指针中，从而避免这个问题。例如：

```
class HeapOnly {
public:
    HeapOnly() {}

    static HeapOnly* Create() { return new HeapOnly(); }
    static void Destroy(HeapOnly* instance) { delete instance; }

private:
    ~HeapOnly() {}
};
```