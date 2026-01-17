# this 关键字
### 通过他，我们可以访问成员函数，成员函数就是属于某个类的函数或方法
### 在函数内部，可以引用this， this是指向-->这个函数所属的当前对象实例的指针；因此可以在c++中写一个非静态的方法，先实例化一个对象，然后去调用这个方法，因此这个方法必须由一个有效对象来调用，而this关键字就是指向那个对象的指针

<img width="1210" height="389" alt="image" src="https://github.com/user-attachments/assets/5c705b04-7449-4f4a-ac78-bb50ebda4e3f" />

## 用法1
<details>
<summary>this 关键字</summary>

```cpp
#include <iostream>
#include <string>

class Entity
{
public:
    int x,y;

    Entity (int x,int y)   //创建构造函数，接收x，y
    {
        //如果不使用初始化成员变量写x(x),y(y),那么在这里里面x=x没有意义，真正要做的是引用属于这个类的成员x和y
        //this就是指向当前对象的指针
        Entity* e = this;
        e->x = x;   //用后面这个x 给指针指向的那个对象的成员变量赋值
        //简写
        this->x = x;        //其实就是先解引用这个指针,拿到他指向的对象的本体，然后去访问这个对象本体的成员变量x  (*this).x = x
        this->y = y;
    }

    int GetX() const    //这个函数后面加了const 说明不可以修改这个类
    {
        const Entity* e = this;
        return x; 
    }
};

int main()
{
    std::cin.get();
}
```
</details>

## 用法2
### 在类的内部调用一个外部函数，然后这个函数接受一个这个类类型作为参数    ---- 把“当前正在被创建的这个对象”传给外面的函数
### 用到 this 的根本原因不是因为“你在内部调用外部”，而是因为：外部那个函数需要访问你的数据，所以你必须把你的地址（this）交给它，它才能找到你。

<img width="1238" height="675" alt="image" src="https://github.com/user-attachments/assets/447d4376-81cb-4eb5-9d1d-7ebb373bbe86" />
<img width="1198" height="788" alt="image" src="https://github.com/user-attachments/assets/cb6bd5c3-a749-477e-98b7-cbb22ba4d610" />


<details>
<summary>this指针用法2</summary>

```cpp
#include <iostream>
#include <string>

void PrintEntity(const Entity& e);  //函数声明

class Entity
{
public:
    int x,y;

    Entity (int x,int y)   //创建构造函数，接收x，y
    {
        //如果不使用初始化成员变量写x(x),y(y),那么在这里里面x=x没有意义，真正要做的是引用属于这个类的成员x和y
        //this就是指向当前对象的指针
        Entity* e = this;
        e->x = x;   //用后面这个x 给指针指向的那个对象的成员变量赋值
        //简写
        this->x = x;        //其实就是先解引用这个指针,拿到他指向的对象的本体，然后去访问这个对象本体的成员变量x  (*this).x = x
        this->y = y;

        Entity& e = *this;   //在非const函数中，通过解引用this，可以赋值给Entity&

        PrintEntity(*this);    //传递Entity类的当前实例到这个函数里面  用this

    }

    int GetX() const    //这个函数后面加了const 说明不可以修改这个类
    {
        const Entity& e = *this;      //加const保证不修改这个类
        return x; 
    }
};

void PrintEntity( const Entity& e)
{
    //Print
}

int main()
{
    std::cin.get();
}
```
</details>

<img width="745" height="424" alt="image" src="https://github.com/user-attachments/assets/ae547a29-c57d-4935-9158-c9b6fb310861" />
