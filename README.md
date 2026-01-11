# c-
practise and record

//单例模式两种写法

class Singleton {
    static Singleton* s_Instance; // 1. 只是在类里"宣称"有这么个变量
};

// 2. 必须在类外面给它分配"实际的内存空间"
Singleton* Singleton::s_Instance = nullptr;

<img width="631" height="194" alt="image" src="https://github.com/user-attachments/assets/ddfd0c49-4899-41f0-a794-fccdc9cbc768" />

//第二种写法正确

<img width="1214" height="449" alt="image" src="https://github.com/user-attachments/assets/b0f31310-c078-49bb-9b59-af2b45f0254b" />

//正确且代码干净的写法：

#include <iostream>
class Singleton
{
//在get函数内创建静态Singleton实例
public:
static Singleton& Get()
{
static Singleton instance;
return instance;
}
void Hello() {}
};
int main()
{
Singleton::Get().Hello();
}
