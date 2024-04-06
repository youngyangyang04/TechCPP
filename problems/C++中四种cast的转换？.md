

1. **static_cast**： `static_cast` 是用于编译时检测到的相关类型之间的转换，比如整型和浮点数、派生类和基类之间的指针或引用转换。它不能用于含有虚函数的多态基类指针或引用到派生类的转换，因为这需要运行时信息。

   示例：

   ```
   int i = 10;
   float f = static_cast<float>(i);    // 整型到浮点数的转换
   ```

2. **dynamic_cast**： `dynamic_cast` 主要用于处理多态性。当涉及到继承体系中的向下转换（将基类的指针或引用转换为派生类类型）时，这个转换会检查转换的安全性。如果转换无效，对于指针，它会返回nullptr；对于引用，则抛出一个`std::bad_cast`异常。使用`dynamic_cast`需要运行时类型信息（RTTI），因此它有一定的性能代价。

   示例：

   ```
   Base* b = new Derived();   // 基类指针指向派生类对象
   Derived* d = dynamic_cast<Derived*>(b);   // 向下转型成功
   if (d) {
       // 转型有效，'d' 不是 nullptr
   }
   ```

3. **const_cast**： `const_cast` 用于移除或添加`const`或`volatile`属性。通常情况下，它被用于移除对象的常量性，允许修改原本被声明为`const`的变量。需要注意的是，去除一个本质上确实是常量的对象的`const`标记并进行修改可能会导致未定义行为。

   示例：

   ```
   const int ci = 10;
   int& modifiable = const_cast<int&>(ci);   // 移除常量性以便修改
   modifiable = 20;  // 注意：如果原对象真的是const，这里可能是未定义行为
   ```

4. **reinterpret_cast**： `reinterpret_cast` 是最危险的cast，它能够执行低级的强制类型转换。尽管几乎没有任何语义检查，但它能够在几乎任意两种类型之间转换，例如整数与指针之间的转换。由于它的不安全性，应该尽可能避免使用`reinterpret_cast`，除非你完全理解所进行的转换。

   示例：

   ```
   int* p = new int(65);
   char* ch = reinterpret_cast<char*>(p);  // 强制指针类型转换
   ```

总结：

- `static_cast`在相关类型间做安全转换。
- `dynamic_cast`在类层次结构中转换，并支持运行时检查。
- `const_cast`改变类型的`const`或`volatile`限定。
- `reinterpret_cast`进行低级别、不安全的强制类型转换。