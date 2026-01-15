# new keyword new关键字
#### 先写new 然后写上数据类型，可以是一个类，可以是基本类型，又或是一个数组；根据所写的类型，以字节为单位决定了要分配的内存大小；
#### 找到连续的内存块，找到之后，他就会返回一个指向那个内存地址的指针；然后就可以开始使用数据，存储或者访问，或读或写
#### 总结：new 就是找到一个满足我们需求的足够大的连续内存块，然后给我们一个指向那个内存地址的指针

<details>
<summary>new 关键字</summary>

```cpp
//39-new keyword
#include <iostream>
#include <string>

using String = std::string;

class Entity
{
private:
    String m_Name;
public:
    Entity() :m_Name("Unknown") {}
    Entity(const String& name) :m_Name(name) {}  //结构函数

    const String& GetName() { return m_Name;}
};

int main()
{
    int a =2;
    int* b = new int[50];  //1）使用new关键字在堆上创建来选择动态分配内存     在堆上分配4字节的整数，b存储的就是他的内存地址
                           //数组 50个 那就是4*50=200个字节 200bytes
    Entity* e = new Entity; //使用new关键字在堆上分配Entity类   new Entity()  括号可以省略，因为他有默认构造函数
    //Entity* e = new(b) Entity;   //这样写可以指定一个内存地址，比如 b
    delete e;
    delete[] b;

    std::cin.get();
}
```
</details>

