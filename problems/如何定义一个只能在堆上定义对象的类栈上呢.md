**只能在堆上创建对象的类**

要实现这一点，我们需要将它的析构函数设置为私有。此外，我们需要提供一个public的接口来删除这个对象。

```C++
class HeapOnly {
private:
    ~HeapOnly() {}  // 私有析构函数

public:
    static HeapOnly* CreateInstance() {
        return new HeapOnly();
    }

    static void DeleteInstance(HeapOnly* p) {
        delete p;
    }
};
```

在这个例子中，我们不能在栈上创建`HeapOnly`类的对象，因为析构函数是私有的。但我们仍然可以在堆上创建，并且需要调用`DeleteInstance()`来删除这个对象。

**只能在栈上创建对象的类**

要实现这一点，我们可以将new操作符重载设为私有。这样就无法使用`new`来在堆上创建对象了。

```c++
class StackOnly {
private:
    void* operator new(size_t size) = delete;  // 禁用new操作符
    void operator delete(void* p) = delete;  // 禁用delete操作符

public:
    StackOnly() {}
    ~StackOnly() {}
};
```

在这个例子中，我们不能在堆上创建`StackOnly`类的对象，因为new操作符已被私有化，但我们仍然可以在栈上创建。