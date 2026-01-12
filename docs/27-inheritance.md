# Inhetitance 继承  （类的继承）
## 展现现有类和为基类提供新功能的一种方式
### 继承使得类之间有了相互关联的层级关系  ————使我们有一个包含通用功能的积累，从最开始的父类中创建出许多派生类
### 将所有通用功能放到一个父类中    ————把一些列所有通用功能的代码放到基类中

### 多态：使用一个单一的符号来表示多个不同类型

<details>
<summary>Player 继承 Entity</summary>

```cpp
#include <iostream>

class Entity
{
public:
    float X,Y;

    void Move(float xa,float ya)  //给每个Entity移动的能力
    {
        X += xa;
        Y += ya;
    }
};

class Player : public Entity  //我们想让Player也可以移动  Player不仅是Player类型，他也是Entity类型 也就是说他同时是两种类型
{
public:                       //对于Player类来说，任何只要不是private的Entity成员，他都可以访问
    const char* Name;
    
    void PrintName()
    {
        std::cout<<Name<<std::endl;
    }

};

int main()
{
    Player player; //创建一个player实例
    player.PrintName(); //调用Player类的PrintName函数
    player.Move(5.0f,5.0f); //调用从Entity类继承过来的Move函数
    player.X = 10.0f; //访问从Entity类继承过来的X成员变量 
    std::cin.get();
}
```
</details>

### Player 总是 Entity 的一个超集！ 创建一个子类 会包含父类的所有内容
