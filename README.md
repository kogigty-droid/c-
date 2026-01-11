# c-
practise and record

//单例模式两种写法

class Singleton {
    static Singleton* s_Instance; // 1. 只是在类里"宣称"有这么个变量
};
// 2. 必须在类外面给它分配"实际的内存空间"
Singleton* Singleton::s_Instance = nullptr;

<img width="631" height="194" alt="image" src="https://github.com/user-attachments/assets/ddfd0c49-4899-41f0-a794-fccdc9cbc768" />


