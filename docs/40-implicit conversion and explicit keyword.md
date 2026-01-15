# implicit conversion and explicit keyword 隐式构造函数、隐式转换、explicit关键字

### c++允许编译器对代码进行一次隐式转换，如果使用一种数据类型作为另外一种数据类型来使用，在这两种类型之间就会有类型转换，c++允许隐式的转换，不需要cast等作隐式转换
### 注意：只能做一次隐式转换

### explicit 关键字   ---禁用隐式转换
#### 如果你想用一个整数构造一个Entity对象，你就必须显示的调用这个构造函数；explicit会禁用隐式转换，explicit关键字放在构造函数前面，这就意味着构造函数不会进行隐式转换
#### 写低级封装的时候，会用上，他可以防止偶然转换和导致性能问题或者bug

<details>
<summary>隐式转换 与 explicit 关键字</summary>

```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    std::string m_Name;
    int m_Age;
public:
    Entity(const std::string& name)
        :m_Name(name),m_Age(-1) {}
    explicit Entity(int age)
        :m_Name("Unknown"),m_Age(age) {}

};

void PrintEntity (const Entity& entity)
{
    //Printing
}

int main()
{     
    PrintEntity(22);   //可以这样写的原因，会发生一次隐式转换 22调用Entity构造函数，转换为 Entity类型
    PrintEntity(std::string("Cherno"));   //隐式转换 std::sting-->Entity

    Entity a = std::string("Cherno");   //隐式转换 std::sting-->Entity
    Entity b = 22;                      //隐式转换 int-->Entity
    // Entity b = 22;   这里无法做到隐式转换，因为explicit禁用了这个构造函数的隐式转换
    std::cin.get();
}
```
</details>

