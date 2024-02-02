当两个对象相互引用并使用`shared_ptr`时，就会形成循环引用。例如，考虑一个简单的场景：

```
#include <memory>
#include <iostream>

class B; // 前置声明

class A {
public:
    std::shared_ptr<B> b_ptr;
    A() { std::cout << "A constructor" << std::endl; }
    ~A() { std::cout << "A destructor" << std::endl; }
};

class B {
public:
    std::shared_ptr<A> a_ptr;
    B() { std::cout << "B constructor" << std::endl; }
    ~B() { std::cout << "B destructor" << std::endl; }
};

int main() {
    std::shared_ptr<A> a = std::make_shared<A>();
    std::shared_ptr<B> b = std::make_shared<B>();
    
    a->b_ptr = b;
    b->a_ptr = a;

    return 0;
}
```

在这个例子中，类 `A` 拥有一个指向类 `B` 的 `shared_ptr`，而类 `B` 拥有一个指向类 `A` 的 `shared_ptr`。这样就形成了循环引用。

为了避免循环引用，我们可以改用 `weak_ptr` 来解决这个问题：

```
#include <memory>
#include <iostream>

class B; // 前置声明

class A {
public:
    std::shared_ptr<B> b_ptr;
    A() { std::cout << "A constructor" << std::endl; }
    ~A() { std::cout << "A destructor" << std::endl; }
};

class B {
public:
    std::weak_ptr<A> a_weak_ptr;  // 使用 weak_ptr
    B() { std::cout << "B constructor" << std::endl; }
    ~B() { std::cout << "B destructor" << std::endl; }
};

int main() {
    std::shared_ptr<A> a = std::make_shared<A>();
    std::shared_ptr<B> b = std::make_shared<B>();
    
    a->b_ptr = b;
    b->a_weak_ptr = a;  // 使用 weak_ptr

    return 0;
}
```

通过将类 `B` 中指向类 `A` 的指针改为 `weak_ptr`，我们成功地避免了循环引用问题。