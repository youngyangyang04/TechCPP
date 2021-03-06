
# volatile作用

Volatile关键词的第一个特性：易变性。所谓的易变性，在汇编层面反映出来，就是两条语句，下一条语句不会直接使用上一条语句对应的volatile变量的寄存器内容，而是重新从内存中读取。

Volatile关键词的第二个特性：“不可优化”特性。volatile告诉编译器，不要对我这个变量进行各种激进的优化，甚至将变量直接消除，保证程序员写在代码中的指令，一定会被执行。
Volatile关键词的第三个特性：”顺序性”，能够保证Volatile变量间的顺序性，编译器不会进行乱序优化。
C/C++ Volatile变量，与非Volatile变量之间的操作，是可能被编译器交换顺序的。C/C++ Volatile变量间的操作，是不会被编译器交换顺序的。哪怕将所有的变量全部都声明为volatile，哪怕杜绝了编译器的乱序优化，但是针对生成的汇编代码，CPU有可能仍旧会乱序执行指令，导致程序依赖的逻辑出错，volatile对此无能为力
针对这个多线程的应用，真正正确的做法，是构建一个happens-before语义。


# static

控制变量的存储方式和可见性。

(1)修饰局部变量

一般情况下，对于局部变量是存放在栈区的，并且局部变量的生命周期在该语句块执行结束时便结束了。但是如果用static进行修饰的话，该变量便存放在静态数据区，其生命周期一直持续到整个程序执行结束。但是在这里要注意的是，虽然用static对局部变量进行修饰过后，其生命周期以及存储空间发生了变化，但是其作用域并没有改变，其仍然是一个局部变量，作用域仅限于该语句块。

(2)修饰全局变量

对于一个全局变量，它既可以在本源文件中被访问到，也可以在同一个工程的其它源文件中被访问(只需用extern进行声明即可)。用static对全局变量进行修饰改变了其作用域的范围，由原来的整个工程可见变为本源文件可见。

(3)修饰函数

用static修饰函数的话，情况与修饰全局变量大同小异，就是改变了函数的作用域。

(4)C++中的static

如果在C++中对类中的某个函数用static进行修饰，则表示该函数属于一个类而不是属于此类的任何特定对象；如果对类中的某个变量进行static修饰，表示该变量为类以及其所有的对象所有。它们在存储空间中都只存在一个副本。可以通过类和对象去调用。

# const的含义及实现机制

 const名叫常量限定符，用来限定特定变量，以通知编译器该变量是不可修改的。习惯性的使用const，可以避免在函数中对某些不应修改的变量造成可能的改动。

(1)const修饰基本数据类型

 1.const修饰一般常量及数组

 基本数据类型，修饰符const可以用在类型说明符前，也可以用在类型说明符后，其结果是一样的。在使用这些常量的时候，只要不改变这些常量的值便好。

 2.const修饰指针变量*及引用变量&

如果const位于星号*的左侧，则const就是用来修饰指针所指向的变量，即指针指向为常量；

如果const位于星号的右侧，const就是修饰指针本身，即指针本身是常量。

(2)const应用到函数中,

 1.作为参数的const修饰符

 调用函数的时候，用相应的变量初始化const常量，则在函数体中，按照const所修饰的部分进行常量化,保护了原对象的属性。
 [注意]：参数const通常用于参数为指针或引用的情况;

 2.作为函数返回值的const修饰符

 声明了返回值后，const按照"修饰原则"进行修饰，起到相应的保护作用。

(3)const在类中的用法

不能在类声明中初始化const数据成员。正确的使用const实现方法为：const数据成员的初始化只能在类构造函数的初始化表中进行
类中的成员函数：A fun4()const; 其意义上是不能修改所在类的的任何变量。

(4)const修饰类对象，定义常量对象
常量对象只能调用常量函数，别的成员函数都不能调用。

# extern

在C语言中，修饰符extern用在变量或者函数的声明前，用来说明“此变量/函数是在别处定义的，要在此处引用”。

注意extern声明的位置对其作用域也有关系，如果是在main函数中进行声明的，则只能在main函数中调用，在其它函数中不能调用。其实要调用其它文件中的函数和变量，只需把该文件用#include包含进来即可，为啥要用extern？因为用extern会加速程序的编译过程，这样能节省时间。

在C++中extern还有另外一种作用，用于指示C或者C＋＋函数的调用规范。比如在C＋＋中调用C库函数，就需要在C＋＋程序中用extern “C”声明要引用的函数。这是给链接器用的，告诉链接器在链接的时候用C函数规范来链接。主要原因是C＋＋和C程序编译完成后在目标代码中命名规则不同，用此来解决名字匹配的问题。

