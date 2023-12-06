1. **Public**:
   - 使用`public`标签指定的成员可以被任何访问该类对象的代码访问。
   - 公开成员定义了类的外部接口。
2. **Protected**:
   - 使用`protected`标签指定的成员只能被以下几种代码访问：
     - 类本身内部的成员函数。
     - 继承自该类的派生类中的成员函数。
   - 保护成员通常用于在基类和派生类之间共享数据或行为，同时对类的其他使用者隐藏这些细节。
3. **Private**:
   - 使用`private`标签指定的成员只能被类本身内部的成员函数（以及其友元）访问。
   - 私有成员是实现类内部封装的关键，防止了对类实现细节的外部访问。

下面是一个简单的类声明示例，展示了如何使用这三种不同的访问说明符：

```c++
class MyClass {
public:    // 公开成员
    int publicVariable;

    void publicMethod() {
        // ...
    }

protected: // 保护成员
    int protectedVariable;

    void protectedMethod() {
        // ...
    }

private:   // 私有成员
    int privateVariable;

    void privateMethod() {
        // ...
    }
};
```