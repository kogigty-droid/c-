# 学习内容

//单例模式两种写法
```cpp
class Singleton {
    static Singleton* s_Instance; // 1. 只是在类里"宣称"有这么个变量
};

// 2. 必须在类外面给它分配"实际的内存空间"
Singleton* Singleton::s_Instance = nullptr;
```
<img width="631" height="194" alt="image" src="https://github.com/user-attachments/assets/ddfd0c49-4899-41f0-a794-fccdc9cbc768" />

//第二种写法正确

<img width="1214" height="449" alt="image" src="https://github.com/user-attachments/assets/b0f31310-c078-49bb-9b59-af2b45f0254b" />

//正确且代码干净的写法：
```cpp
#include <iostream>

class Singleton 
{
//在get函数内创建静态Singleton实例
public:
    static Singleton& Get()        //尤其这里是返回的引用 那么下面少了stati 将会是打问题
    { 
        static Singleton instance; //假设去掉static  会有问题：Singleton实例会在栈上创建
        return instance; 
    }                              //运行到这个花括号 退出这个函数作用域就会被销毁
    void Hello() {}
};


int main()
{
    Singleton::Get().Hello();
    
    std::cin.get();
}
```
<img width="429" height="494" alt="image" src="https://github.com/user-attachments/assets/a84d8d43-1c38-46e0-8022-b4e1ef3cdfae" />
## 会有问题：
