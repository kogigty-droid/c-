# function pointer 函数指针

###  注： auto function = Print;  
//OK!，去掉括号就不是在调用这个函数，而是在获取函数指针，得到了这个函数的地址。就像是带了&取地址符号一样"auto function = &Print;""(隐式转换)。
C++ 规则：函数名在赋值时自动退化为函数指针（地址）。 


### () 在 C++ 中被称为“函数调用操作符” 

<img width="850" height="400" alt="image" src="https://github.com/user-attachments/assets/16d19589-085f-431f-9d23-98f745174c82" />

### &：     auto function = &HelloWord        在这里auto的实际类型是 void(*function)
在这个可执行文件中，找到这个函数，我们来获取那些cpu指令的内存地址

### 类型别名：
```cpp
typedef void(*HelloWorldFunction)();
HelloWorldFunction function = HelloWorld;
```

<img width="1150" height="585" alt="image" src="https://github.com/user-attachments/assets/31964867-7e39-4f08-9c1e-9080c127ef82" />

<img width="811" height="443" alt="image" src="https://github.com/user-attachments/assets/fbcc35d1-551c-4428-9543-96f2f4b51b5e" />

```cpp
using HelloWorldFunction = void(*)();
HelloWorldFunction function = HelloWorld;
```

<img width="1184" height="405" alt="image" src="https://github.com/user-attachments/assets/373b31a3-0600-4b39-baae-d241217df099" />

```cpp
// 编译器自动推导 function 的类型为 void(*)()
auto function = HelloWorld;
```

<img width="1131" height="234" alt="image" src="https://github.com/user-attachments/assets/e6f4872f-3f89-40f8-945b-ec8b76097f03" />

