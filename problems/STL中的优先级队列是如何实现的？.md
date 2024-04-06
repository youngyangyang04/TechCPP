在 C++ STL 中，`std::priority_queue` 默认情况下使用 `std::vector` 作为其底层容器，并且使用 `std::make_heap`、`std::push_heap` 和 `std::pop_heap` 算法来维护堆的性质。

`std::priority_queue` 允许用户指定一个比较函数对象，这个比较对象定义了元素的优先级。默认情况下，它使用 `std::less<T>`，这意味着队列使用最大堆，最大的元素总