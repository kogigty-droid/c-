## enums 枚举  只能用整型
<img width="640" height="741" alt="image" src="https://github.com/user-attachments/assets/482c5a0e-377f-4e00-a3d0-5e3418e70a78" />
在以上情况下，我希望可以定义一种数据类型，使得他的值只能在这三个值中的某一个值，（因为只要在main函数中int value=具体的  那么后面的都没意义了），而且可以以把这些数据组合起来。
这就是枚举的使用场景了
```cpp
enum Example
{   //声明example为新的数据类型，称为枚举(enumeration);
 A, B, C   //声明A, B, C等为符号常量，通常称之为枚举量，其值默认分别为0，1，2，默认从0开始依次递增 若A = 5， 后面就是6,7....
};

int a = 0;
int b = 1;
int c = 2;

int main ()
{
    Example value = 1;    //这里的赋值必须是枚举的三个值之一
    if (value = B)
    {
    }
    std::cin.get();
}
```
## Log类中的枚举应用
```cpp
#include <iostream>

class Log
{
public:
    enum Level
    {
        Error = 0,      //三个枚举值
        Warning = 1,
        Info = 2
    };
private:
    int m_LogLevel = Info;
public:
    void SetLevel(Level level)   //枚举出来的新类型 Level   之前是int level
    {
        m_LogLevel = level;      //level的值只能是那三个之一
    }

    void Error1(const char* message)     //这条信息是字符串
    {
        if (m_LogLevel >= Error)
            std::cout << "[ERROR]: " << message << std::endl;
    }

    void Warning1(const char* message)
    {
        if (m_LogLevel >= Warning)
            std::cout << "[WARNING]: " << message << std::endl;
    }

    void Info1(const char* message)
    {
        if (m_LogLevel >= Info)
            std::cout << "[INFO]: " << message << std::endl;
    }

};

int main()
{
    Log log;
    log.SetLevel(Log::Warning); //这里这么写的原因是：Error枚举值是在Log类命名空间的，而枚举类型Level本身不是一个命名空间
    
    //这里注意 枚举值的命名可能和函数名同名，会冲突
    log.Info1("This is an info message.");
    log.Warning1("This is a warning message.");
    log.Error1("This is an error message.");

    std::cin.get();
}
```
