# 结构体Constructors
## 在c++ 中，必须手动初始化所有数据类型
## 构造函数不会在你没有实例化对象的时候运行，因此，如果只是使用类的静态方法，构造函数是不会执行的
## 代码示例：
## 
<details>
<summary>结构体 数据类型初始化</summary>
<pre>
```cpp
//结构体
#include <iostream>

class Entity
{
public:
    float X, Y;
    //按照以下创建初始化方法的话，main函数中每次实例化一个对象都要调用这个函数，会使代码冗杂
    // void Init()  //这里需创建一个初始化方法
    // {
    //     X = 0.0f;
    //     Y = 0.0f;
    // }
    //解决思路：当我们创建Enity对象的时候，能自动运行这个初始化方法就好了————用构造函数，那是一种特殊类型的方法。   
    Entity()    //构造函数：函数名和类名相同，没有返回值
    {
        X = 0.0f;
        Y = 0.0f;
    }
    
    void Print()  
    {
    std::cout << X << ", " << Y << std::endl;
    }
};

int main()
{
    Entity e;   
    e.Print();    //实例化Entity之后调用Print函数
    std::cin.get();
}
</pre>
</details>
```

## 如果你不指定构造函数，你仍然有一个构造函数，这叫做默认构造函数（default constructor），是默认就有的。但是，我们仍然可以删除该默认构造函数：
<details>
<summary>删除默认构造函数示例</summary>
<pre>
```cpp
class Log{
public:
    Log() = delete;  //删除默认构造函数
    ......
}
</pre>
</details>
```
