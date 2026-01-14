# create instantiate objects 创建实例化对象
### 实例化类的两种方式  --区别在于内存来自哪里，我们的对象实际上会创建在哪里。
#### 类中有很多成员，他们必须被存储在某个地方，决定开始使用这个变量时，会创建很多变量，这个对象有很多的变量，我们需要电脑在某个地方进行内存分配，这样就可以记住这些变量的值
##### 堆和栈上面创建对象的一些不同的功能差异：
比如：栈对象有一个自动的生存周期，他们的生存周期是由他声明的地方的作用域决定的；一旦超出了这个作用域，他的内存就会别释放掉。因为当作用域结束时，栈会弹出；在这个栈上，这个作用域的所有东西都会被释放
但是堆却不一样，他很神秘！！一旦你在堆上分配一个对象，实际上你已经在堆上创建了一个一直存在那里的对象。直到你决定不需要它，想释放这个对象

#### 空作用域
<img width="1149" height="566" alt="image" src="https://github.com/user-attachments/assets/650c0c72-a492-48ce-b11f-a198bdab8d56" />

#### 栈
<img width="1350" height="575" alt="image" src="https://github.com/user-attachments/assets/7c3f77ef-7189-4444-89e8-a7dd58467e0b" />

<img width="940" height="288" alt="image" src="https://github.com/user-attachments/assets/216ce545-9d26-4859-a4d6-065553f0ffa5" />

#### 对象不能在栈上分配的一些原因：
<img width="1245" height="380" alt="image" src="https://github.com/user-attachments/assets/c7f62955-49de-49e9-8b22-81f669cdec1a" />

<details>
<summary>对象在栈上分配</summary>

```cpp
#include <iostream>
#include <string>

using String = std::string; //类型别名  使用String代替std::string  简化代码

class Entity
{
private:
    String m_Name;
public:
    Entity () : m_Name("Unknown") {}     //默认构造函数
    Entity (const String& name) : m_Name(name) {} //接受一个字符串参数的构造函数

    const String& GetName() const { return m_Name; }

};

int main()
{
    Entity* e;     //创建一个Entity类型的指针，e就是一个指向Entity的变量
    {
        Entity entity("Cherno"); //在这个作用域内创建一个Entity对象  名字是Cherno
        e = &entity;  //把这个对象(在栈上创建的对象)的地址赋值给指针e
    }     //当代码运行到这一行的时候，那个角entity的对象就被销毁了，因为它是在栈上创建的

    //因此 想要这个对象Entity entity("Cherno");在作用域外仍然存活的话，我们不能把它分配到栈上，而必须分配到堆上
    //如果entity太大，或者有很多个，也不能在栈上分配；栈通常很小，一般是一两兆。
    std::cout<<e.GetName()<<std::endl;
    std::cin.get();
}
```
</details>

### 堆上分配对象：
<img width="1330" height="106" alt="image" src="https://github.com/user-attachments/assets/f63a9aac-2024-4d46-9f82-331f9694a29c" />

<details>
<summary>堆上分配对象</summary>
```cpp
#include <iostream>
#include <string>

using String = std::string; //类型别名  使用String代替std::string  简化代码

class Entity
{
private:
    String m_Name;
public:
    Entity () : m_Name("Unknown") {}     //默认构造函数
    Entity (const String& name) : m_Name(name) {} //接受一个字符串参数的构造函数

    const String& GetName() const { return m_Name; }

};

int main()
{
    Entity* e;     //创建一个Entity类型的指针，e就是一个指向Entity的变量
  
    {
    Entity* entity = new Entity("Cherno"); //在堆上创建一个Entity对象  名字是Cherno  在堆上分配，类型不再是Entity，而是Entity*
    //new Entity实际上发生的就是在堆上分配了内存；我们调用了Entity的构造函数，然后这个new Entity实际上会返回一个Entity指针，它返回了这个entity在堆上被分配的内存地址
    //在堆上分配对象的话，你必须手动去释放分配的内存
    e = entity;
    }
    std::cout<<e->GetName()<<std::endl;
    std::cin.get();

    delete e;      //delete + 变量名（对象）
    
}
```
</details>






