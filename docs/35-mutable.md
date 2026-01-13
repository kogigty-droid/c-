# mutable  可改变的东西

#### const std::string& GetName() const { return m_Name; }  第一个const是保证引用这个n_Name是只读的，第二个const是让GetName方法承诺它是只读的  
#### 可能用到mutable的情况：假设为了调试，要计算这个函数在程序里被调用了多少次，需要一个m_DebugCount的整型，初始化为0

<details>
<summary>mutable应用</summary>
```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    std::string m_Name;
    mutable int m_DebugCount;
public:
    const std::string& GetName() const  //返回一个常量引用，防止修改
    {   
        m_DebugCount++; //即使在const函数中也能修改m_DebugCount  但需要现在定义成员变量那里，显然他是mutable的
        return m_Name;
    }
};
int main ()
{
    Entity e;
    e.GetName();
    std::cin.get();
}
```
</details>


### 另外一个用到mutable的地方 lambda
<img width="1101" height="690" alt="image" src="https://github.com/user-attachments/assets/1fe267ae-79b5-478f-bcbb-aab723b44e0d" />
