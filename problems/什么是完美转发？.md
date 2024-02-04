完美转发是一个与模板和函数重载相关的概念，它允许一个函数将其接收到的参数以原始的值类别（左值或右值）传递给另一个函数。这意味着**如果你传递了一个左值给包装函数，那么被调用的函数也会接收到一个左值；如果传递的是一个右值，则同样地，被调用的函数会接收到一个右值。**



```
#include <utility>

// 这个函数负责“转发”它的参数到另一个函数
template<typename T>
void wrapper(T&& arg) {
    // 使用 std::forward 来确保 arg 的值类别得以保持不变
    target(std::forward<T>(arg));
}

// 一个可能接受左值或右值参数的目标函数
void target(int& x) {
    // 处理左值
}

void target(int&& x) {
    // 处理右值
}

int main() {
    int lv = 5;     // 左值
    wrapper(lv);    // 应该调用 void target(int& x)
    wrapper(10);    // 应该调用 void target(int&& x)
}

```

