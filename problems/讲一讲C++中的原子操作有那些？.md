在C++中，原子操作是由 `<atomic>` 头文件提供的一组操作和类型，它们确保了在多线程环境中对共享数据的修改是不可分割的，即这些操作在执行过程中不会被其他线程打断。原子操作主要用于实现无锁（lock-free）编程，允许多个线程安全地并发访问和修改数据。



`std::atomic` 是C++11引入的一个模板类，用来封装任意类型（满足TriviallyCopyable）的值，并且保证对这些值的操作是原子的。以下是一些常见的原子操作：

1. `store`：将值写入原子对象。
2. `load`：从原子对象读取值。
3. `exchange`：替换原子对象的值，并返回该对象之前的值。
4. `compare_exchange_weak` / `compare_exchange_strong`：比较原子对象的值，并在相等时替换为新值。
5. `fetch_add` / `fetch_sub`：对原子对象进行加/减操作，并返回操作前的值。
6. `fetch_and` / `fetch_or` / `fetch_xor`：对原子对象进行位与/位或/位异或操作，并返回操作前的值。
7. `++` / `--`：原子地递增或递减对象的值。



原子操作还包括一些内存顺序（memory order）的概念，如 `memory_order_relaxed`, `memory_order_consume`, `memory_order_acquire`, `memory_order_release`, `memory_order_acq_rel`, `memory_order_seq_cst`。这些内存顺序用于控制操作的执行顺序，以及如何处理编译器和处理器级别的优化。