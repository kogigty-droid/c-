# const 关键字

##### 绕开const的方法： 强制转换：

```cpp
  const int Age =90;
  int* a = new int;
  *a = 2;    //1.改变指针指向的内存内容
  a = &Age //error!
  a =(int*)&Age //ok   //改变指针指向的内存地址   把Age的地址取出来给到a
```
<details>
<summary>没有const的声明</summary>

```cpp
int main ()
{
    const int MAX_AGE = 90;  //常量  不可修改
    int* a = new int;  //在堆上创建一个整型，这个声明没有做const  因此可以做两件事
    *a = 2;      //1)解引用a 并赋值为2
    a = (int*)&MAX_AGE;  //2)重新分配指针（改变指针a指向的内存地址）  让a指向另一个地址    不建议强制转换
    std::cout << *a << std::endl;

}
```
</details>

<img width="1213" height="469" alt="image" src="https://github.com/user-attachments/assets/4534430b-c38b-436a-9e71-295414255b2f" />

## 区分 指向常量的指针 与 常量指针
### 关键：const在指针*前还是在 *后。   
#### *后：常量指针-->  "int* const a"     *前： 指向常量的指针-->  "int const* a"  或者 "const int* a"
#### 指向常量的常量指针：（const既在指针*前又在指针*后）  "const int* const a"
#### ----既不能改变指针的内容，也不能改变指针本身让他指向别处。

### const 第三中用法： 放在方法名的后面
<details>
<summary>const 放在方法名后</summary>
```cpp
#include <iostream>
#include <string>

class Entity
{
private:
    int m_X, m_Y;
    mutable int var;  //mutable关键字允许即使在const成员函数中也能修改这个变量
public:
    int GetX() const   //在成员函数后面加const，表示这个函数不会修改类的任何成员变量 (可读不可写)
    {
        var = 2;  //即使在const函数中也能修改var
        return m_X;
    }  

    void SetX(int x)
    {
        m_X = x;
    }
};

void PrintEntity(const Entity& e)    //写个函数可以访问方法   //常量引用 不想复制
{
    std::cout<<e.GetX()<<std::endl;   
    //std::cout<<e.SetX()<<std::endl;  //由于上面参数是引用Entity，因此对于会改变Entity的函数都不能调用
}
int main ()
{

    Entity e;
    const int MAX_AGE = 90;  //const常量  不可修改
    const int* a = new int();
    *a = 2;
    a = (int*)&MAX_AGE;
    std::cout<<*a<<std::endl;
}
```
</details>


#### 注：如果要变指针，那么都要加*  如：int a,b; ————> 变成指针: int* a, *b;



   
