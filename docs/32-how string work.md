# 字符串 character  占用1字节
#### 它可以把指针转换为char类型指针，让你可以根据字节进行指针运算；若想分配1k内存，可以分配1024个char；1字节=8bit
#### 空终止符 00 可以让我们知道字符串在哪终止
<img width="1340" height="420" alt="image" src="https://github.com/user-attachments/assets/39ca7776-351b-4dbd-b7a4-3ee58e3a991b" />

#### 字符数组打印的时候不知道在什么时候终止，可以在尾部加个 '\0' ，打印就不会在后面出现乱码
#### std::string本质上就是basic_string的char作为模板参数的模板类实例
#### 双引号包含的内容是const char数组，不是真正的string，他不是字符串，不能将两个指针或两个数组加在一起
#### 复制字符串意味着必须在堆上动态的穿件全新的char数组来储存我们之前已经得到的完全相同的文本；因此传入一个只读字符串的时候，确保通过常量引用传递他

<details>
<summary>字符串的使用</summary>

```cpp
//字符串的使用：
#include <iostream>
#include <string>

void PrintString(const std::string& string)  //传引用更高效   //const确保不会修改它，&确保不会复制它
{
    std::cout<<string<<std::endl;
}
int main()
{
    //char* name = "Hello";
    // //name[2] = 'a';   //试图修改字符串常量的内容
    // std::string name = "Hello";  // +"Cherno"  双引号包含的内容是const char数组，不是真正的string，他不是字符串，不能将两个指针或两个数组加在一起
    // name += " Cherno";  //字符串拼接

    //或者显示调用string构造函数，将其中一个传入string构造函数中
    std::string name = std::string ("Hello") + " Cherno";
    //查找字符串中的文本
    bool contains = name.find("llo") != std::string::npos; //npos表示未找到  是否是非法位置
    std::cout<<name<<std::endl;

    std::cin.get();
}
```
</details>
