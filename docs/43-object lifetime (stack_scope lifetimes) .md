# object lifetime (stack_scope lifetimes) 对象的生存周期
### 内存和对象是怎么在栈上生存的       基于栈的变量生存周期是什么意思
#### 栈就是你可以在他顶部添加东西的数据结构，就如桌子上有一落书，要拿中间的书，需要把上面的几本书拿掉；每进入一个作用域，我们就是在push栈帧，也不一定就是一个栈帧
### 基于栈和基于堆的变量生存周期的区别： 
#### 基于栈的变量，在我们离开作用域的时候会被销毁，内被被释放；基于堆的不会
#### 注： 数组即指针： 在 C++ 中，数组名在很多情况下会“退化”为指向该数组第一个元素的指针
####      凡是在函数内部（比如 main 函数）声明的变量，如果没有用 new 关键字来修饰这个变量本身，它默认就是分配在栈（Stack）上的

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
<summary>错误及更正后的的代码</summary>

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
    CreateArray(array);        //数组名“退化” ,隐式转换  数组名array-->“指向第一个元素的指针”
    
    {
        Entity* e = new Entity();
    }
    std::cin.get();
}
```
</details>

<img width="790" height="325" alt="image" src="https://github.com/user-attachments/assets/d78cd5c5-2b49-4f5f-9e44-07dc23b3d373" />

### 在栈上创建东西的一些使用地方： 
#### 比如利用类的作用域来实现的，像只能指针smart_ptr 或是 作用域指针unique_ptr,这是一个作用域指针 或者像作用域锁
#### 例如作用域指针，本质上就是一个类，是一个指针的包装器，在构造时在堆上分配指针，在析构时删除指针，可以自动化这个new 和delete 

#### 作用域指针：
<img width="984" height="675" alt="image" src="https://github.com/user-attachments/assets/e592fa11-c3a6-4395-b6b8-c04d561e4406" />
<img width="699" height="405" alt="image" src="https://github.com/user-attachments/assets/6bd5928e-f2be-4ca6-bcaf-fcd2b1688b75" />

<details>
<summary>智能指针 Scope_Ptr</summary>

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

class ScopePtr
{
private:
    Entity* m_Ptr;   //这是一个指向Entity对象的指针 在 ScopePtr 这个类内部，保存一个 Entity 对象的内存地址 这里仅仅是声明我有这么一个变量而已
public:
    ScopePtr (Entity* ptr)   //创建一个构造函数 接受一个指针
        : m_Ptr(ptr)         //把这个ptr赋值给m_Ptr
    {
    }

    ~ScopePtr()           //在析构函数中调用delete删除m_Ptr
    {
        delete m_Ptr;      //delete m_Ptr 就可以间接的把Entity这个对象销毁  可以把这块内存释放
    }
};

int main()
{
    {
        //希望在跳出作用域时能够自动删除他   可以使用c++标准库中的作用域指针 ScopePtr
        //注意：凡是在函数内部（比如 main 函数）声明的变量，如果没有用 new 关键字来修饰这个变量本身，它默认就是分配在**栈（Stack）**上的
        ScopePtr e = new Entity();  //ScopePtr e 声明了一个类型为 ScopePtr 的局部变量 e
        //ScopePtr e：是栈对象（管理者） new Entity()：是堆对象（被管理者）。
        
        Entity* e = new Entity();     
    }
    std::cin.get();
}
```
</details>


### 一些知识点
<img width="1110" height="518" alt="image" src="https://github.com/user-attachments/assets/51a9b281-8a01-4578-8968-2ea7b86d2b55" />
<img width="979" height="565" alt="image" src="https://github.com/user-attachments/assets/a32e45ae-ccee-44b5-8065-9da0b0ed185e" />
<img width="930" height="550" alt="image" src="https://github.com/user-attachments/assets/931f6df3-ce04-4878-b21b-28642f520d1d" />

#### delete m_Ptr; 能清理堆内存，是因为 delete 是一个功能强大的操作符，它不仅通过指针找到了堆内存的地址，还负责触发了清理逻辑（析构函数）和归还逻辑（释放内存）。执行delete m_Ptr的时候，delete操作符很聪明，他找到了这个m_Ptr是一个Entity类型，知道这个指针上住着一个Entity对象，它会立即跳转到堆内存中该对象的地址，并强制执行该对象的析构函数 ~Entity()

#### 应用例子：自动计时器
##### 一个计时器，加入你想计算在你基准测试范围内的时间，可以写一个timer类，在对象创建构造时开始计时，然后再对象销毁时停止计时，并且打印出计时；函数开头加上一行代码，那么整个作用域就会被计时，不需要手动去停止计时器。一旦超出作用域他就会停止。




