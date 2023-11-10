下面是一个简单的示例（以C++ 03为例）

注意在写的时候，针对于指针资源的配置与释放需要尤其注意，以及字符串的自赋值。这是写的时候比较容易出错的两个关键点，切记。

```C++
class MyString {
private:
    char* m_Data;
    int m_Length;

public:
    // 默认构造函数
    MyString() : m_Data(new char[1]), m_Length(0) {
        m_Data[0] = '\0';
    }

    // 参数化构造函数
    MyString(const char* str) {
        m_Length = strlen(str);
        m_Data = new char[m_Length + 1];
        strcpy(m_Data, str);
    }

    // 拷贝构造函数
    MyString(const MyString& other) {
        m_Length = other.m_Length;
        if (m_Length > 0) {
            m_Data = new char[m_Length + 1];
            strcpy(m_Data, other.m_Data);
        } else {
            m_Data = new char[1];
            m_Data[0] = '\0';
        }
    }

    // 析构函数
    ~MyString() {
        delete[] m_Data;
    }
    
    // 拷贝赋值运算符
    MyString& operator=(const MyString& other) {
        
        // 注意！
        if (&other == this) {
            return *this;
        }

        delete[] m_Data;
        m_Length = other.m_Length;
        if (m_Length > 0) {
            m_Data = new char[m_Length + 1];
            strcpy(m_Data, other.m_Data);
        } else {
            m_Data = new char[1];
            m_Data[0] = '\0';
        }
        
        return *this;
    }
};

```

