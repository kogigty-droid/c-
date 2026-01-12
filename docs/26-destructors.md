# 析构函数
## 与构造函数对比：
### 构造函数在你创建一个对象实例的时候运行，析构函数是在你销毁一个对象实例的时候运行
### 构造函数:需要设置变量或初始化工作的时候被调用
### 析构函数：释放任何内容，或者需要清理任何内存的时候适用；同样适用于栈和堆分配的内存

<details>
<summary>析构函数应用</summary>
    
```cpp
//结构体
#include <iostream>

class Entity
{
public:
    float X, Y;
    Entity()    //构造函数：函数名和类名相同，没有返回值
    {
        X = 0.0f;
        Y = 0.0f;
        std::cout<<"created Entity"<<std::endl;
    }

    ~Entity()   //析构函数：函数名和类名相同，前面加个~     //main函数结束时会自动调用析构函数
    {
        std::cout<<"destroyed Entity"<<std::endl;
    }
void Print()  
    {
    std::cout << X << ", " << Y << std::endl;
    }
};

void Function()    //这个函数做Entity的所有操作
    {
        Entity e;
        e.Print();
    }

int main()
{
    // Entity e;    //这里就可以使用参数来构造Entity
    // e.Print();    //实例化Entity之后调用Print函数
    Function(); 
    std::cin.get();
}
```
</details>

