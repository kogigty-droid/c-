# operators and operator overloading  操作符与操作符重载

#### 操作符：基本上就是我们用来代替函数执行某些事情的符号，不仅仅是数学运算符，还有一些其他常用的运算符，例如解引用（deference）操作符；箭头运算符；+=运算符；取址运算符；左移操作符，即两个左尖括号，用来把东西打印到cout，也就是控制台上；new和delete也是操作符
#### 总而言之，操作符就是函数
#### 操作符重载：重载的意思就是给他一个新的含义，或者增加参数，或者重新创建；重载允许你在程序中定义或者更改一个操作符的行为!

### 不使用操作符重载的情况
<details>
<summary>不使用操作符重载</summary>

```cpp
#include<iostream>
#include<string>

struct Vector2     //因为需要字段都是public的，所以就写成结构体
{
    float x,y;
    Vector2 (float x,float y)      //定义一个向量的构造函数，比如（1，3）
        :x(x),y(y) {}
    
    Vector2 Add(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x+other.x,y+other.y);         //返回你做的加法的值
    }

    Vector2 Multiply(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x*other.x,y*other.y);         //返回你做的乘法的值
    }
};

int main()
{   
    //储存一个位置和速度
    Vector2 position(4.0f,4.0f);    //也许是表示位置的向量
    Vector2 speed(0.5f,1.5f);       //也许是表示速度的向量
    Vector2 powerup(1.1f,1.1f);     //增加量 

    //若不使用重载操作符:
    //Vector2 result = position.Add(speed);       //调用叠加函数   speed的向量+position的向量
    //假设还需要通过某种方式来改变我们的speed  也许是快10%或其他  作用与speed 做一个成倍的增加

    Vector2 result = position.Add(speed.Multiply(powerup));   //这个Multiplay函数就是为了实现成倍增加 


    std::cin.get();
}
```
</details>



### 1.使用操作符重载
<details>
<summary>操作符重载</summary>

```cpp
#include<iostream>
#include<string>

struct Vector2     //因为需要字段都是public的，所以就写成结构体
{
    float x,y;
    Vector2 (float x,float y)      //定义一个向量的构造函数，比如（1，3）
        :x(x),y(y) {}
    
    Vector2 Add(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x+other.x,y+other.y);         //返回你做的加法的值
    }

    //操作符重载情况：
    Vector2 operator+(const Vector2& other) const          //操作符重载情况 ， 参数传入别的向量
    {
        return Add(other);         //返回你做的加法的值 直接调用Add函数，因为他实现的就是这个功能
    }

    Vector2 Multiply(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x*other.x,y*other.y);         //返回你做的乘法的值
    }
    
    //操作符重载情况：
    Vector2 operator*(const Vector2& other) const          //操作符重载情况 ， 参数传入别的向量
    {
        return Multiply(other);         //返回你做的乘法的值 直接调用Multiply函数，因为他实现的就是这个功能
    }

};

int main()
{   
    //储存一个位置和速度
    Vector2 position(4.0f,4.0f);    //也许是表示位置的向量
    Vector2 speed(0.5f,1.5f);       //也许是表示速度的向量
    Vector2 powerup(1.1f,1.1f);     //增加量 

    //若不使用重载操作符:
    //Vector2 result = position.Add(speed);       //调用叠加函数   speed的向量+position的向量
    //假设还需要通过某种方式来改变我们的speed  也许是快10%或其他  作用与speed 做一个成倍的增加

    Vector2 result1 = position.Add(speed.Multiply(powerup));   //这个Multiplay函数就是为了实现成倍增加 
    Vector2 result2 = position + speed * powerup;   //使用操作符重载来实现这个功能   需要先定义+ 和 * 这两个操作符
 


    

    std::cin.get();
}
```
</details>

### 2.左移操作符的重载
#### "<<"操作符  << 接受两个参数，一个是输出流cout，另一个是Vector2
#### 对于 "<<" 可以在类外进行重载，因为他和Vector2这个类没什么关系   //重载操作符的原始定义 std::ostream&

<img width="1341" height="614" alt="image" src="https://github.com/user-attachments/assets/0833703e-97b1-4f9e-905a-723ba051e688" />

<details>
<summary>左操作符</summary>

```cpp
#include<iostream>
#include<string>

struct Vector2     //因为需要字段都是public的，所以就写成结构体
{
    float x,y;
    Vector2 (float x,float y)      //定义一个向量的构造函数，比如（1，3）
        :x(x),y(y) {}
    
    Vector2 Add(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x+other.x,y+other.y);         //返回你做的加法的值
    }

    //操作符重载情况：
    Vector2 operator+(const Vector2& other) const          //操作符重载情况 ， 参数传入别的向量
    {
        return Add(other);         //返回你做的加法的值 直接调用Add函数，因为他实现的就是这个功能
    }

    Vector2 Multiply(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x*other.x,y*other.y);         //返回你做的乘法的值
    }
    
    //操作符重载情况：
    Vector2 operator*(const Vector2& other) const          //操作符重载情况 ， 参数传入别的向量
    {
        return Multiply(other);         //返回你做的乘法的值 直接调用Multiply函数，因为他实现的就是这个功能
    }

};

    //对于 "<<" 可以在类外进行重载，因为他和Vector2这个类没什么关系   //重载操作符的原始定义 std::ostream&
    std::ostream& operator<<(std::ostream& stream,const Vector2& other)
    {
        stream << other.x <<"," << other.y;
        return stream;
    }

int main()
{   
    //储存一个位置和速度
    Vector2 position(4.0f,4.0f);    //也许是表示位置的向量
    Vector2 speed(0.5f,1.5f);       //也许是表示速度的向量
    Vector2 powerup(1.1f,1.1f);     //增加量 

    //若不使用重载操作符:
    //Vector2 result = position.Add(speed);       //调用叠加函数   speed的向量+position的向量
    //假设还需要通过某种方式来改变我们的speed  也许是快10%或其他  作用与speed 做一个成倍的增加

    Vector2 result1 = position.Add(speed.Multiply(powerup));   //这个Multiplay函数就是为了实现成倍增加 
    Vector2 result2 = position + speed * powerup;   //使用操作符重载来实现这个功能   需要先定义+ 和 * 这两个操作符
    std::cout << result2 <<std::endl;          //"<<"操作符  << 接受两个参数，一个是输出流cout，另一个是Vector2

    

    std::cin.get();
}
```
</details>

### 3.bool操作符的重载

<img width="995" height="323" alt="image" src="https://github.com/user-attachments/assets/2612bf0b-ec5d-470b-963d-5ef2cc3a1591" />

<details>
<summary>bool操作符</summary>

```cpp
#include<iostream>
#include<string>

struct Vector2     //因为需要字段都是public的，所以就写成结构体
{
    float x,y;

    Vector2 (float x,float y)      //定义一个向量的构造函数，比如（1，3）
        :x(x),y(y) {}
    
    Vector2 Add(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x+other.x,y+other.y);         //返回你做的加法的值
    }

    //操作符重载情况：
    Vector2 operator+(const Vector2& other) const          //操作符重载情况 ， 参数传入别的向量
    {
        return Add(other);         //返回你做的加法的值 直接调用Add函数，因为他实现的就是这个功能
    }

    Vector2 Multiply(const Vector2& other) const          //参数传入别的向量
    {
        return Vector2(x*other.x,y*other.y);         //返回你做的乘法的值
    }
    
    //操作符重载情况：
    Vector2 operator*(const Vector2& other) const          //操作符重载情况 ， 参数传入别的向量
    {
        return Multiply(other);         //返回你做的乘法的值 直接调用Multiply函数，因为他实现的就是这个功能
    }

    bool operator==(const Vector2& other) const     //只是做了比较，不会修改类
    {  
        return x == other.x && y == other.y;
    }
    
    bool operator!=(const Vector2& other) const     //只是做了比较，不会修改类
    {  
        return !(*this == other);
    }
};

    //对于 "<<" 可以在类外进行重载，因为他和Vector2这个类没什么关系   //重载操作符的原始定义 std::ostream&
std::ostream& operator<<(std::ostream& stream,const Vector2& other)
{
    stream << other.x <<"," << other.y;
    return stream;
}

int main()
{   
    //储存一个位置和速度
    Vector2 position(4.0f,4.0f);    //也许是表示位置的向量
    Vector2 speed(0.5f,1.5f);       //也许是表示速度的向量
    Vector2 powerup(1.1f,1.1f);     //增加量 

    //若不使用重载操作符:
    //Vector2 result = position.Add(speed);       //调用叠加函数   speed的向量+position的向量
    //假设还需要通过某种方式来改变我们的speed  也许是快10%或其他  作用与speed 做一个成倍的增加

    Vector2 result1 = position.Add(speed.Multiply(powerup));   //这个Multiplay函数就是为了实现成倍增加 
    Vector2 result2 = position + speed * powerup;   //使用操作符重载来实现这个功能   需要先定义+ 和 * 这两个操作符
    std::cout << result2 <<std::endl;          //"<<"操作符  << 接受两个参数，一个是输出流cout，另一个是Vector2
    
    if (result1 == result2)
    {
        std::cout << "same" << std::endl;
    }
    

    std::cin.get();
}
```

</details>
