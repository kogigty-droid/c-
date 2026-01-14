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

#### 别的类也可以作为自己的成员变量
<img width="893" height="470" alt="image" src="https://github.com/user-attachments/assets/ff0caf8d-9810-454c-9fea-00e7084912c6" />
<img width="1054" height="330" alt="image" src="https://github.com/user-attachments/assets/471f3d2f-f2c3-4fb4-940b-554dd1dee022" />

#### 初始化成员变量并调用函数的两种写法：
#### 1.: m_Example(8)     ----直接初始化           这是标准化写法
过程：编译器直接找到 Example 类中接受 int 参数的构造函数（即 Example(int x)），并在 m_Example 的内存位置上直接调用它。

#### 2.: m_Example(Example(8))  ----拷贝构造        啰嗦复杂
过程：1）调用 Example(int) 创建临时对象。
      2）调用 Example(const Example&) 或 Example(Example&&) 复制/移动给成员。
      3）调用 ~Example() 析构临时对象。





