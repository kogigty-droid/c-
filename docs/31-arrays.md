# 数组
### 1.指针是数组如何工作的基础知识；数组就像在一个变量里面有多个变量
### 2.数组中的数据是连续的
#### 如果只想打印数组，而不是他的元素，那么只会打印出来他的内存地址，因为他实际是一个指针！ 

<img width="644" height="641" alt="image" src="https://github.com/user-attachments/assets/3d096275-4562-4220-b30a-bd4d799345cd" />
<img width="886" height="569" alt="image" src="https://github.com/user-attachments/assets/b82f7eea-44c9-42d5-b20d-90e3494a80a8" />

<details>
<summary>数组</summary>

```cpp
#include <iostream>

int main()
{
  int example[5];
  int* ptr = example;
  example[2] = 5; //访问元素2号，然后给他赋值5，结果就是会写入从指针偏移8字节的内存中
  *(ptr + 2) =6;  //利用指针重写，然后解引用 等同于上面那种写法
}
```
</details>

<img width="860" height="459" alt="image" src="https://github.com/user-attachments/assets/b3cf44df-f23f-4a50-b5c5-daaa8a52ad09" />
<img width="1285" height="841" alt="image" src="https://github.com/user-attachments/assets/21cd83b4-fc76-43d8-b8c0-51dfe6f6833a" />

#### c++的数组中无法计算大小，只能通过 sizeof(example)/sizzeof(int) ————个数 (假设是整型)
