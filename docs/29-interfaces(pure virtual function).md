#  interface 关键字
## 在c++中 通过 “纯虚函数 + 抽象类” 模拟接口：c++中的纯虚函数本质上和其他语言（比如Java和c#）中的抽象方法和接口相同
#### 在面向对象程序设计中，创建一个只包含未实现方法然后交由子类去实际实现功能的类是非常普遍的————这通常称为接口
#### 接口———— 只包含未实现的方法并作为一个模板类
#### 由于此接口类实际上不包含方法实现，所以无法实例化这个类

<img width="1070" height="446" alt="image" src="https://github.com/user-attachments/assets/fe251418-cb56-43f9-9842-687ade19e1a3" />

<details>
<summary>纯虚函数实例代码</summary>
    
```cpp
#include <iostream>
#include <string>

class Printable                     //Printable 这个类型来保证有GetClassName这个函数
{
public:
    virtual std::string GetClassName() = 0;   //纯虚函数  无法实例化 需要通过子类Entity来实现
};

class Entity : public Printable    //实现接口
{
public:
    virtual std::string GetName() { return "Entity"; }   
    std::string GetClassName() override { return "Entity"; }   
    
};

class Player : public Entity
{
private:
    std::string m_Name;  
public:
    Player(const std::string& name)   
     : m_Name(name) {}        
    
    std::string GetName() override        
    {
        return m_Name;
    }

    std::string GetClassName() override { return "Player"; }
};

void PrintName(Entity* entity)
{
    std::cout<<entity->GetName()<<std::endl;
}

void Print(Printable* obj)     //里面需要有一种类型，来保证有GetClassName这个函数   接受Printable对象
{
    std::cout << obj->GetClassName()<< std::endl;
}

int main()
{
    Entity* e = new Entity();  
    //PrintName(e);
    

    Player* p = new Player("Hero");  
    //PrintName(p);
    
    // Entity* entity = p; 
    // PrintName(entity);
    
    Print(e);
    Print(p);

    std::cin.get(); 
}
```
</details>
