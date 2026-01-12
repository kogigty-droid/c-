# 虚函数  virtual Functions
### 虚函数可以让我在子类中重写方法： 在父类中新建一个方法并把它标记为虚函数,我们就可以在子类中重写这个方法去做其他的事情
### 注意： 当写 new Entity() 的时候，程序会在堆（head）上分配一块内存，new运算符返回的是这块内存的地址，在c++中存储地址的变量必须是指针
### 必须用指针接收地址： Entity* e = new Entity();
### ptr->GetName()   意思是：把ptr指针指向的对象抓出来，然后再对这个抓出来的对象调用函数  ————(*ptr).GetName

#### new(堆内存)
<img width="1120" height="500" alt="image" src="https://github.com/user-attachments/assets/4f675f6e-f1ff-4284-b118-86d37674bc88" />
<img width="781" height="165" alt="image" src="https://github.com/user-attachments/assets/3b49db9d-a000-4467-b0f8-d9ed763bd324" />

#### 参数类型是 Entity* ,意味着他只会在函数内部寻找和调用GetName，想要调用子类中Player的GetName,就需要用到虚函数；需要把基类中的原函数设置为虚函数
#### 虚函数引入了一种需要动态分派的东西，一般通过虚表（vtabel）来实现编译；利用override关键字对进行了重写的函数进行标记
<img width="875" height="575" alt="image" src="https://github.com/user-attachments/assets/836a71dd-2f68-4dfe-863f-df602b597645" />

<details>
<summary>虚函数示例</summary>

```cpp
//虚函数
#include <iostream>
#include <string>

class Entity
{
public:
    virtual std::string GetName()   //设置为虚函数，若是在子类中进行了修改，可以被找到
    {
        return "Entity";
    }
};

class Player : public Entity
{
private:
    std::string m_Name;   //先给他一个m_Name,然后再给他一个构造函数，来更改这个名字
public:
    
//“定义一个构造函数，它接收一个只读的字符串引用。在对象创建的同时，直接把这个字符串塞给成员变量 m_Name，而不需要在函数体里再折腾一次赋值。”
    Player(const std::string& name)   //构造函数： 函数名和类名相同，没有返回值  引用（&）的目的：高效传输（借来看看）
     : m_Name(name) {}        //成员初始化列表的方法，更高效 ；//在 Player 对象被创建出来的那个瞬间，直接用 name 构造好m_Name
    
    std::string GetName() override         //这个就可以用来修改m_Name 利用override关键字对进行了重写的函数进行标记
    {
        return m_Name;
    }
};

void PrintName(Entity* entity)
{
    std::cout<<entity->GetName()<<std::endl;
}

int main()
{
    Entity* e = new Entity();  
    PrintName(e);
     
    Entity* p = new Player("Hero");  //用父类的指针指向子类的对象
    PrintName(p);

    Entity* entity = p; //entity是一个Entity类型的指针，但是我们把它指向了一个Player类型
    PrintName(entity);
    
    std::cin.get(); //“暂停程序等待你按回车”。如果你没按回车，或者没关掉那个终端窗口，程序就一直占用着 main.exe 这个文件
}
```
</details>
