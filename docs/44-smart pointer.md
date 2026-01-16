# smart pointer 智能指针 std--unique_ptr  std--shared_ptr  std--weak_ptr
### 智能指针就是说当你调用new分配内存的时候，你不用自己去调用。实际上在很多使用智能指针的情况下，甚至不用去调用new。
#### 智能指针其实就是对原始指针的包装。当你创建一个智能指针，他会调用new 为你分配内存，然后基于你使用的智能指针，分配的内存会在某一时刻自动释放。
### 1.最简单的智能指针 unique_ptr 作用域指针：当这个指针超出作用域时，他就会被销毁，就会调用delete。
#### unique_ptr必须是unique的，不能copy一个unique_ptr,如果copy的话，他们会指向同一个内存地址，当你其中一个unique_ptr指针die的时候，他就是释放那块内存，指向相同内存地址的第二个unique_ptr就会指向已经被释放的内存
### 要使用这些智能指针，需要先引入<memory>头文件 

#### 注意：隐式转换 std::unique_ptr<Entity> entity= new Entity()；不能使用隐式转换原因： new Entity()返回的是裸指针Entity*，而左边的是智能指针对象std::unique_ptr<Entity> entity； =：是在告诉编译器：“请帮我隐式地把右边的这个裸指针（内存地址），包装成左边的智能指针对象（类对象）。然而，std::unique_ptr 的构造函数中有explicit 关键字，说明这个构造函数只能显式调用，不能用于隐式转换。      很显然 类对象≠指针

### std::unique_ptr<Entity> 是 C++ 标准库定义的一个模板类（Template Class）。虽然我们叫它“智能指针”，但它不是指针，它是一个对象

#### std::unique_ptr<Entity>这个标准类里面就是要求传入一个指针

<img width="1055" height="453" alt="image" src="https://github.com/user-attachments/assets/66e9bdfa-d8f6-4154-b4c0-f78070f0c6d9" 
    />
<img width="1061" height="380" alt="image" src="https://github.com/user-attachments/assets/8dbc518a-e9ee-40bf-930c-0c8f953ae81d" />

<img width="1200" height="678" alt="image" src="https://github.com/user-attachments/assets/61a211cf-f9a3-4f6c-904a-52e6acf4d81b" />

### 最好的做法：出于异常安全考虑：    最终不会因为得到一个没有引用空指针而导致内存泄露
#### 把entity赋值为std::make_unique<Entity>()，即：std::unique_ptr<Entity> entity = std::make_unique<Entity>();

<details>
<summary>作用域指针</summary>

```cpp
#include <iostream>
#include <string>
#include <memory>

class Entity
{
public:
    Entity()
    {
        std::cout << "Created Entity" << std::endl;
    }

    ~Entity()
    {
        std::cout << "Destroyed Entity" << std::endl;
    }

};

int main()
{   

    {
        //在main函数的特定作用域里面创建一个unique_ptr
        //unique_ptr的构造函数是explicit的  不可以用隐式转换，需要显示调用构造函数
        std::unique_ptr<Entity> entity(new Entity()); //传入一个模板参数<Entity> 给他一个名字 比如 entity ，传入new Entity()来调用他的构造函数
        //隐式转换 std::unique_ptr<Entity> entity= new Entity()
        //不能使用隐式转换原因： new Entity()返回的是裸指针Entity*，而左边的是智能指针对象std::unique_ptr<Entity> entity； =：是在告诉编译器：“请帮我隐式地把右边的这个裸指针，包装成左边的智能指针对象。
        //std::unique_ptr 的构造函数中有explicit 关键字，说明这个构造函数只能显式调用，不能用于隐式转换 

        //出于异常安全考虑，另外一种方式是把entity赋值为std::make_unique<Entity>();  这是最好的做法
        std::unique_ptr<Entity> entity = std::make_unique<Entity>();
    }
    std::cin.get(); 
} 
```
</details>

### 2.共享指针
#### 工作方式是通过引用计数,引用计数是一种跟踪统计你的指针有多少次引用的方法，一旦计数为0，他就会被删除
#### 大概过程：我创建了一个shared_ptr,然后copy他创建了另外一个shared_ptr,那么引用计数就是2，当我一个指针die的时候，我的引用计数-1，现在就是一个计数，当我最后一个指针die的时候，我的引用计数回到0，整个就die了

### unique_ptr不直接调用new 的原因是异常安全，但是在shared_ptr中不直接调用new的原因不一样：
#### shared_ptr会额外分配一块叫控制块的内存，用来储存引用计数，如果你先创建一个 new Entity(),然后传给shared_ptr的构造函数，那总共机会有两次内存分配，显示new Entity()的内存分配，然后是shared_ptr控制块的内存分配------------因此，使用make_shared 就可以把两者结合起来，效率更高

<img width="1375" height="681" alt="image" src="https://github.com/user-attachments/assets/6a88b56b-34cf-4bff-b734-146f2b4368a5" />

### 3.weak_ptr 弱指针  可以和shared_ptr 一起使用
#### 作用：可以像声明任何东西那样声明他，这里当你把share_ptr赋值给weak_ptr的时候，他不会增加引用计数，如果不想获得Entity的所有权，这将非常有用
#### 就像你在对一个Entity列表进行排序，你并不真正关心他们是否有效，你只需要存储他们的一个引用就好，可以通过weak_ptr去判断底层对象是否还活着。因为他不会增加引用计数，所以它不会保证底层对象一直活着

<details>
<summary>智能指针</summary>

```cpp
#include <iostream>
#include <string>
#include <memory>

class Entity
{
public:
    Entity()
    {
        std::cout << "Created Entity" << std::endl;
    }

    ~Entity()
    {
        std::cout << "Destroyed Entity" << std::endl;
    }

    void Print()
    {
        
    }

};

int main()
{   

    // {
    //     //在main函数的特定作用域里面创建一个unique_ptr
    //     //unique_ptr的构造函数是explicit的  不可以用隐式转换，需要显示调用构造函数
    //     std::unique_ptr<Entity> entity(new Entity()); //传入一个模板参数<Entity> 给他一个名字 比如 entity ，传入new Entity()来调用他的构造函数
    //     //隐式转换 std::unique_ptr<Entity> entity= new Entity()
    //     //不能使用隐式转换原因： new Entity()返回的是裸指针Entity*，而左边的是智能指针对象std::unique_ptr<Entity> entity； =：是在告诉编译器：“请帮我隐式地把右边的这个裸指针，包装成左边的智能指针对象。
    //     //std::unique_ptr 的构造函数中有explicit 关键字，说明这个构造函数只能显式调用，不能用于隐式转换 

    //     //出于异常安全考虑，另外一种方式是把entity赋值为std::make_unique<Entity>();  这是最好的做法
    //     std::unique_ptr<Entity> entity = std::make_unique<Entity>();

    //     //shared_ptr
    //     std::shared_ptr<Entity> sharedEntity = std::make_shared<Entity>();
    //     //或者另外一种写法：显示调用，传入指针：
    //     std::shared_ptr<Entity> sharedEntity (new Entity());
    // }


    {
        std::weak_ptr<Entity>  e0;      //创建一个弱指针  叫e0
        {
            std::shared_ptr<Entity> sharedEntity = std::make_shared<Entity>();
            e0 = sharedEntity;
        }
    }


    std::cin.get(); 
} 
```
</details>

<img width="1279" height="558" alt="image" src="https://github.com/user-attachments/assets/f8b340fc-6c06-478e-b9ef-194da4797423" />

### “知道对象已经死了” 这件事本身，就是 weak_ptr 存在的巨大意义。核心作用主要体现在两个方面：安全地检查存活 和 打破循环引用。
