在C++中，单例模式是一种设计模式，用来限制一个类只能创建一个对象。这对于需要全局访问点的情况非常有用，例如日志记录或者数据库连接。

下面是一个简单的单例模式的实现

```C++
class Singleton {
private:
    static Singleton* instance;
    // 私有构造函数，防止从其他地方创建对象。
    Singleton() {}

public:
    // 静态访问方法。
    static Singleton* getInstance() {
        if (instance == 0) {
            instance = new Singleton();
        }
        return instance;
    }
};

// 初始化指针为零，这样在第一次调用getInstance时可以初始化
Singleton* Singleton::instance = 0;

int main() {
    // 创建一个新的Singleton对象。
    Singleton* s = Singleton::getInstance();
   
    // 使用Singleton对象。

    return 0;
}

```

