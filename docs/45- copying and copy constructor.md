# copying and copy constructor   复制与拷贝构造函数

### 注：对于<<字符串重载问题，之所以要对他进行重载的原因在于对于你自己定义的类 比如String，std::cout根本不认识他   
#### 用new的原因：

<img width="1116" height="216" alt="image" src="https://github.com/user-attachments/assets/4db7a9c1-8c33-4832-8614-f3ba37782647" />

## 默认的复制 浅拷贝    ------没有申请新内存
###   String string = "Cherno"; String second = string;  //复制字符串
#### 在复制字符串时，c++会自动为我们获取这里的所有成员，这些成员基本上就是这个类的组成部分，他获取这些值，并把它们复制到second的新内存地址里面，现在内存中就有两个String，由于他执行的是直接复制(称为浅拷贝)，所以他复制了这个指针，所以内存中的两个字符串，他们的char*完全相同。即m_Buffer的内存地址，对于两个String来说是相同的。    
#### 崩溃原因，执行到末尾时，当两个字符串被销毁时，析构函数被调用，最终导致m_Buffer被删除了两次。两次试图释放同一块内存 不行的

<img width="914" height="349" alt="image" src="https://github.com/user-attachments/assets/5cb0fb45-88a5-461f-8161-c545e3ff8ce0" />

#### 浅拷贝的默认构造函数
<img width="1120" height="275" alt="image" src="https://github.com/user-attachments/assets/c40047a2-1b15-46ef-988f-ca4ccf2bf08d" />


### 我们实际希望做到的是复制那块内存，想要我们第二个String-->  有自己的指针，有自己的内存块，这样子，修改或删除第二个String的时候，不会影响第一个String
### 深拷贝     -----将对象完整的复制出来
#### 拷贝构造函数是在实际复制第二个字符串时为该字符串调用的构造函数。  当你试图创建一个新变量，并将其赋值给另一个与你实际创建的变量类型相同的变量时，你实际上是在复制该变量，因此调用了所谓的复制构造函数

<details>
<summary>浅拷贝与深拷贝</summary>

```cpp
#include <iostream>
#include <string>
#include <cstring>

struct Vector2     //结构体亦是如此
{
    float x,y;
};

class String
{
private:
    char* m_Buffer;
    unsigned int m_Size;
public:
    String(const char* string)
    {
        m_Size = strlen(string);
        m_Buffer = new char [m_Size+1];  //“向操作系统申请一块位于【堆内存】的连续空间，大小刚好能装下 m_Size 个字符，然后把这块地盘的地址交给 m_Buffer保管。”
                                         //+1是为了给空终止符腾出空间 
        //将指针中的值复制到实际缓存区中，这样缓存区就会被字符填充
        // for (int i = 0; i < m_Size; i++)
        //     m_Buffer[i] = string[i];
        memcpy(m_Buffer,string,m_Size);    //更简单的写法，参数是目标缓冲区，源缓冲区，大小
        m_Buffer[m_Size] = 0;  //手动在末尾添加自己的空终止符
    }

    //c++默认提供的一个拷贝构造函数   浅拷贝
    // String (const String& other)
    //     :m_Buffer(other.m_Buffer),m_Size(other.m_Size)
    //{}

    //String (const String& other) = delete;   //拷贝构造函数声明为delete  那么就无法进行浅拷贝

    //进行深拷贝 自己写一个拷贝构造函数
    String (const String& other)
        :m_Size(other.m_Size)        //m_Size是一个整数，可以直接进行浅拷贝
    {
        m_Buffer = new char[m_Size + 1];    //简单的分配一个新的缓冲区
        memcpy(m_Buffer,other.m_Buffer,m_Size + 1);
    }

    
    ~String()
    {
        delete[] m_Buffer;
    }

    char& operator[](unsigned int index)    //重写索引  
    {
        return m_Buffer[index];
    }

    friend std::ostream& operator<<(std::ostream& stream,const String& string);
};

std::ostream& operator<<(std::ostream& stream,const String& string)
{
    stream << string.m_Buffer;    // stream指的就是输出流    形象理解： “嘿，cout(stream)！虽然你不认识这个 String 对象，但别急。我把对象里面藏着的那串字符数据（m_Buffer）拿出来给你。这东西你认识吧？请把它打印出来。”
    return stream;
}

void PrintString(const String& string)    //用引用，这样string不会被复制很多次  3  传入的是string这个对象
{
    //如果还想要一个副本的话 可以这样写：
    String copy = string;

    std::cout << string <<std::endl;
}

int main()
{
    // int a = 2;
    // int b = a;     //a b 是两个独立变量 他们有两个不同的内存地址
    // b = 3;         //b 的内存中有两个不同的值

    // Vector2 a = {1,3};
    // Vector2 b = a;
    // b.x = 3;

    Vector2* a = new Vector2();
    Vector2* b = a;              //这里实际上复制的是指针（同一个内存地址），但是他们指向不同的东西   复制的是内存地址而不是那段内存本身的内容
    b->x = 2;     //这会同时影响a和b ，因为他们指向同一个内存地址
    

    String string = "Cherno";
    String second = string;  //复制字符串
    second[2] = 'a';     //将second里的字符串第三个字母改为a  但是正常情况下 只有int[2] = a;这种写法可行   没见过second[2] = a;这种写法  因此需要重写一下这个引用

    // std::cout << string <<std::endl;
    // std::cout << second <<std::endl;
    //直接写一个函数来打印这些
    PrintString(string);
    PrintString(second);
    std::cin.get();
}
```
</details>

## 提示： 总是要使用const引用传递你的对象 ， always
