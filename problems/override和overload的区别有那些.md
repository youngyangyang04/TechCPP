函数重载（Overload）：当一个作用域内有两个或更多个函数名相同但参数列表不同的函数时，我们就说这些函数构成了重载。参数列表不同可以是参数数量不同，也可以是参数类型不同。函数重载使得我们可以使用一样的函数名来完成类似的操作，提高代码的可读性和易用性。

示例：

```c++
void foo(int a);
void foo(double a);
```

函数覆盖（Override）：当一个派生类声明了一个与基类中虚函数完全相同（函数名、参数类型和个数、常量属性、返回值类型）的函数时，我们就说派生类的这个函数覆盖了基类的虚函数。这使得我们可以通过基类指针或引用来调用派生类的函数，实现多态。

示例：

```c++
class Base {
public:
    virtual void foo(int a);
};

class Derived : public Base {
public:
    void foo(int a) override; // 覆盖基类的虚函数foo
};
```

