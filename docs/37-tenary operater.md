# tenary operater  三元运算符
#### 他只是if语句的语法糖


<img width="1339" height="394" alt="image" src="https://github.com/user-attachments/assets/48504a8a-97ad-4da5-b94e-502f8063da64" />
#### 注意区分 static 和 const          
#### static 的变量完全可以被修改，重点是不能别其他cpp文件访问不到
1.static (静态) 是什么意思？static 只有两个作用：   
1）生存期（Memory Duration）：变量在程序启动时分配内存，直到程序结束才释放。
2）可见性（Visibility/Linkage）：这是重点。 它表示这个变量 s_Speed 只在这个 .cpp 文件内部可见。其他的 .cpp 文件即使写了 extern int s_Speed; 也访问不到它。它就像是一个“私有的全局变量”。
它是完全可以被修改的！ 你想怎么改就怎么改。

<details>
<summary>三元运算符</summary>

```cpp
//37-tenary operator 三元运算符
#include <iostream>
#include <string>

static int s_Level = 1;
static int s_Speed = 2;

int main()
{
    // if (s_Level > 5)
    //     s_Speed = 10;
    
    // else
    //     s_Speed = 5; 
    // //使用三元运算符改写上面代码     优势：简短
    // s_Speed = (s_Level > 5) ? 10 : 5;   //如果s_Level大于5，s_Speed赋值为10，否则赋值为5
    
    //使用三元运算符给字符串赋值
    s_Speed = (s_Level > 5) ? (s_Level >10) ? 20 : 10 : 5; //嵌套三元运算符 等级大于10，速度20，等级大于5速度10，否则5
    

    std::string Rank = (s_Level > 5 ) ? "Master" : "Beginner"; //如果s_Level大于5，Rank赋值为"Master"，否则赋值为"Beginner"
    //上面三元运算符，没有构造中间字符串的原因与返回值优化有关！！！


    std::string OtherRank;    //<-- 这里创建了一个变量，因为这种声明方式实际会构造一个空字符串对象，然后又会被后面代码中的字符串对象("Master")覆盖掉      ----> 这种方式会更慢，因为创建了一个临时字符串，然后又立即销毁它。
    if (s_Level > 5)
        OtherRank = "Master";
    else
        OtherRank = "Beginner";
    std::cin.get();


}
```
</details>


