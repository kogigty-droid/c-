# function pointer 函数指针

###  注： auto function = Print;  
//OK!，去掉括号就不是在调用这个函数，而是在获取函数指针，得到了这个函数的地址。就像是带了&取地址符号一样"auto function = &Print;""(隐式转换)。
C++ 规则：函数名在赋值时自动退化为函数指针（地址）。 


### () 在 C++ 中被称为“函数调用操作符” 

<img width="850" height="400" alt="image" src="https://github.com/user-attachments/assets/16d19589-085f-431f-9d23-98f745174c82" />
