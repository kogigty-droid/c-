# 字符串字面量 --双引号中的内容

<img width="710" height="310" alt="image" src="https://github.com/user-attachments/assets/5479cdbf-e49e-480a-bf0d-6a0d36aabe7a" />

#### 字符串字面量总是存储在只读内存中

<details>
<summary>字符串字面量</summary>
  
```cpp
//33-字符串字面量

#include <iostream>
#include <string>

#include <stdlib.h>  //C标准库

int main()

{
    //c++14 的string_literal库里面，有方法实现更简单的字符串相加
    using namespace std::string_literals;  //使用命名空间
    std::string name0 = "Hello"s + "Cherno";  //"s"后缀表示这是一个字符串字面量
    std::wstring name01 = L"Hello"s + L"Cherno";
    std::u32string name02 = U"Hello"s + U"Cherno";

    //忽略转义字符，对打印很多行有帮助
    const char*example = R"(Line 1
    Line 2
    Line 3)";

    const char* name = "Cherno";   //8个元素的字符串
    const wchar_t* name2 = L"Cherno"; //宽字符字符串  每个字符占两个字节  L字符串字面量由宽字符组成
    const char16_t* name3 = u"Cherno"; //每个字符占两个字节  u字符串字面量由UTF-16字符组成
    const char32_t* name4 = U"Cherno"; //每个字符占四个字节  U字符串字面量由UTF-32字符组成

    
    std::cin.get();
}
```
</details>

##### 别的一些字符串：
##### 基本上，char是一个字节的字符，char16_t是两个字节的16个比特的字符（utf16），char32_t是32比特4字节的字符（utf32），const char就是utf8. 
##### 那么wchar_t也是两个字节，和char16_t的区别是什么呢？事实上宽字符的大小，实际上是由编译器决定的，可能是一个字节也可能是两个字节也可能是4个字节，
##### 实际应用中通常不是2个就是4个（Windows是2个字节，Linux是4个字节），所以这是一个变动的值。如果要两个字节就用char16_t，它总是16个比特的。

```cpp
    const char* name = "lk";
    const wchar_t* name2 = L"lk";
    const char16_t* name3 = u"lk";
    const char32_t* name4 = U"lk";
   const char* name5 = u8"lk";
```
