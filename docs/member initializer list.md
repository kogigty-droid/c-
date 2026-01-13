# member initializer list  构造函数初始化列表    

### 在构造函数中初始化类成员的一种方式，当我们编写类并向这个类添加成员的时候，通常需要用某种方式对这些成员进行初始化
### 基本上就是用括号代替等号，然后移动到列表里      

<details>
<summary>成员初始化列表</summary>
  
```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    std::string m_Name;
    int m_Score;
public:
    // Entity()
    //     : m_Name("Unknown") //使用成员初始化列表
    // {
    //     m_Name = "Unknown"; //这种写法效率低，因为先调用了默认构造函数，然后又赋值了一次
    // }

    Entity()
        : m_Name("Unknown") //使用成员初始化列表
    {
    }

    // Entity (const std::string& name)  //这种写法效率低，因为先调用了默认构造函数，然后又赋值了一次
    // {
    //     m_Name = name;
    // }
    
    Entity (const std::string& name)   //使用成员初始化列表
        : m_Name(name)
    {
    }


    const std::string& GetName() const
    {
        return m_Name;
    }

    
};

int main()
{
    Entity e;
    std::cout<<e.GetName()<<std::endl; 
    
    std::cin.get();
} 
```
</details>

#### 好处--干净易读
