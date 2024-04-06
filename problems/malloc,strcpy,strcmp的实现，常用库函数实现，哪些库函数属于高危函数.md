`malloc`：此函数用于在堆上动态分配内存

```c++
void *malloc(size_t size) {
    //sbrk()是一种在C和C++中用于增加或减少程序数据段大小的系统调用。它通过改变堆的末尾地址来改变程序的内存空间。
    //这里的sbrk是一种可能的调用方式，在每个操作系统中不一定相同，具体可以看对应操作系统的底层源码，比如Windows下会调用virtual allocated函数一样
    
    void *p = sbrk(0);
    void *request = sbrk(size);
    if (request == (void*) -1) {
        return NULL; // sbrk failed.
    } else {
        assert(p == request); // Not thread safe.
        return p;
    }
}
```

`strcpy`：此函数用于复制字符串。

```c++
char *strcpy(char *dest, const char *src) {
    char *ret = dest;
    while ((*dest++ = *src++) != '\0')
        ;
    return ret;
}
```

`strcmp`: 此函数用于比较两个字符串。

```c++
int strcmp(const char *str1, const char *str2) {
    while (*str1 && (*str1 == *str2)) {
        str1++;
        str2++;
    }
    return *(unsigned char *)str1 - *(unsigned char *)str2;
}
```

**关于高危函数**

- 一般来说，任何可以导致缓冲区溢出、整数溢出、空指针引用或其他形式的未定义行为的函数都可能是高风险的。在C/C++语言中，一些常见的例子包括`gets()`, `scanf()`, `strcpy()`, `strcat()`, `sprintf()`等，这些函数在使用不当时可能会导致安全问题。
- 对于C++中的STL中来说，使用iterator可能会导致不安全的行为，这个通常会在进行循环的时候会用到，我们一般情况下可以用at()函数或者使用类似于for(auto  element : elements)，以及特定的STL自带的库函数。