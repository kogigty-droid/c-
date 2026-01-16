# object lifetime (stack_scope lifetimes) 对象的生存周期
### 内存和对象是怎么在栈上生存的       基于栈的变量生存周期是什么意思
#### 栈就是你可以在他顶部添加东西的数据结构，就如桌子上有一落书，要拿中间的书，需要把上面的几本书拿掉；每进入一个作用域，我们就是在push栈帧，也不一定就是一个栈帧
### 基于栈和基于堆的变量生存周期的区别： 
#### 基于栈的变量，在我们离开作用域的时候会被销毁，内被被释放；基于堆的不会
#### 注： 数组即指针： 在 C++ 中，数组名在很多情况下会“退化”为指向该数组第一个元素的指针

### 局部作用域创建数组的经典错误
#### 创建一个基于栈的变量，然后返回一个指向他的指针

<details>
<summary>不可工作情况</summary>

```cpp

int* CreateArray()
{
    int array[50];
    return array;    //把数组的首地址（比如地址是 0x1000）返回出去了
}                    //当代码执行到 }（函数结束）时，CreateArray 的栈帧（Stack Frame）被弹出。这意味着系统回收了这块内存

int main()
{   
    //如果在栈上创建数组 int array[50]  下面这个int* a = CreateArray();会出问题 会崩溃
    int* a = CreateArray();  //int* a 接收到了地址 0x1000;但是，当试图通过 a 去访问里面的数据时（比如 a[0]），你是在访问一块已经被销毁、不再属于你的内存

    {
        Entity* e = new Entity();
    }
    std::cin.get();
}
```
</details>


### 两种解决办法 
#### 1.在堆上分配这个数组，就不会被释放   int* array = new int[50];
<img width="945" height="191" alt="image" src="https://github.com/user-attachments/assets/035bb72a-be05-4b91-9f88-c738884cfb0b" />

#### 2.在main函数里面创建数组，然后赋值给作用域外的函数变量

<details>
<summary>错误记更正后的的代码</summary>

```cpp
#include <iostream>
#include <string>

class Entity
{
public:
    Entity()
    {
        std::cout<<"Created Entity"<<std::endl;
    }

    ~Entity()
    {
        std::cout<<"Destroyed Entity"<<std::endl;
    }
};

// int* CreateArray()
// {
//     int array[50];
//     //法1：在堆上创建这个数组
//     int* array = new int[50];
//     return array;    //把数组的首地址（比如地址是 0x1000）返回出去了
// }                    //当代码执行到 }（函数结束）时，CreateArray 的栈帧（Stack Frame）被弹出。这意味着系统回收了这块内存

void CreateArray(int* array)
{
    //fill our array
}
int main()
{   
    //如果在栈上创建数组 int array[50]  下面这个int* a = CreateArray();会出问题 会崩溃
    //int* a = CreateArray();  //int* a 接收到了地址 0x1000;但是，当试图通过 a 去访问里面的数据时（比如 a[0]），你是在访问一块已经被销毁、不再属于你的内存
    
    //法2：在main函数里面创建数组，然后赋值给作用域外的函数变量
    int array[50];
    CreateArray(array);
    
    {
        Entity* e = new Entity();
    }
    std::cin.get();
}
```
</details>
