# the arrow operator  箭头运算符

### 不能通过指针去访问函数

<img width="985" height="300" alt="image" src="https://github.com/user-attachments/assets/76fcee78-03c8-4e6c-8991-7adf0222e040" />

#### 解引用这个指针(*ptr)就可以找到对象-----解引用：顺着地址（指针）找到房子（对象本体）

### operator关键字
#### operator->：这是 C++ 的关键字。它的意思是：“当有人对我的对象使用箭头符号 -> 时，请执行这个函数。

<img width="799" height="380" alt="image" src="https://github.com/user-attachments/assets/e7b60fbc-9468-4a28-a637-43030063430b" />

<details>
<summary>箭头运算符</summary>

```cpp
#include<iostream>
#include<string>

class Entity
{
public:
    int x;
public:
    void Print() const { std::cout <<"Hello" <<std::endl; }

};

class ScopedPtr     //写某种智能指针类     作用域指针类
{
private:
    Entity* m_Obj;   //实体指针
public:        
    ScopedPtr(Entity* entity)    //构造脚本指针时，接收实体指针作为参数
        :m_Obj(entity)
    {
    }

    ~ScopedPtr()                 //析构函数用来删除实体    当实体超出作用域范围时，就会被自动删除
    {
        delete m_Obj;
    }

    //Entity* GetObject () 
    // { 
    //     return m_Obj; 
    // }
    Entity* operator-> () 
    {  
        return m_Obj; 
    }
    
    const Entity* operator-> () const    //常量实体，并将预算符标记为常量
    //“智能指针”承诺了它是只读的，所以它交出来的“裸指针”m_Obj也必须是只读的，而只读的指针只能调用只读的函数。所以：void Print() const { std::cout <<"Hello" <<std::endl; }
    {  
        return m_Obj; 
    }
};
int main()
{   
    // Entity e;  //实例化一个Entity类型的对象 名字叫e
    // e.Print();  //调用这个类里面的函数

    // Entity* ptr = &e;   //假如这个对象是个指针，需要实例化一个指针对象名字叫ptr，然后获取e的内存里的地址 给到ptr
   
    // // Entity& entity = *ptr;    //引用这个实体 
    // // entity.Print();          //没办法通过指针去访问函数，必须通过对象去访问函数

    // //(*ptr).Print();     //简写:解引用这个指针，然后去访问里面的函数
    // ptr->Print();   //利用箭头运算符就可以通过指针去访问到类里面的函数
    // ptr->x = 2;   //访问这个对象里面的x，把它改为2

    const ScopedPtr entity = new Entity();    //用右边entity指针去构造了一个左边ScopePtr  所以实现隐式转换  可以对等
    //entity.GetObject()->Print();      //调用ScopePtr这个类里面的函数GetObject()得到返回的m_Obj指针，然后再去从这个指针对应的Entity类型里面去调用Print()函数
    entity->Print();      //本来对象是天生不支持->的，由于operate关键字让他在看到->的时候能够去return m_Obj；进而实现对Print的调用

    std::cin.get();
}
```
</details>

### delete m_Obj   堆上的内存被销毁的过程
<img width="986" height="575" alt="image" src="https://github.com/user-attachments/assets/0ec7a197-6d7a-4698-a159-9c9d367d5602" />


