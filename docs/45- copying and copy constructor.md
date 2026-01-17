# copying and copy constructor   复制与拷贝构造函数

### 注：对于<<字符串重载问题，之所以要对他进行重载的原因在于对于你自己定义的类 比如String，std::cout根本不认识他   
#### 用new的原因：

<img width="1116" height="216" alt="image" src="https://github.com/user-attachments/assets/4db7a9c1-8c33-4832-8614-f3ba37782647" />

## 默认的复制 浅拷贝    ------没有申请新内存
###   String string = "Cherno"; String second = string;  //复制字符串
#### 在复制字符串时，c++会自动为我们获取这里的所有成员，这些成员基本上就是这个类的组成部分，他获取这些值，并把它们复制到second的新内存地址里面，现在内存中就有两个String，由于他执行的是直接复制(称为浅拷贝)，所以他复制了这个指针，所以内存中的两个字符串，他们的char*完全相同。即m_Buffer的内存地址，对于两个String来说是相同的。    
#### 崩溃原因，执行到末尾时，当两个字符串被销毁时，析构函数被调用，最终导致m_Buffer被删除了两次。两次试图释放同一块内存 不行的

<img width="914" height="349" alt="image" src="https://github.com/user-attachments/assets/5cb0fb45-88a5-461f-8161-c545e3ff8ce0" />

#### 浅拷贝的默认构造函数
<img width="1120" height="275" alt="image" src="https://github.com/user-attachments/assets/c40047a2-1b15-46ef-988f-ca4ccf2bf08d" />


### 我们实际希望做到的是复制那块内存，想要我们第二个String-->  有自己的指针，有自己的内存块，这样子，修改或删除第二个String的时候，不会影响第一个String
### 深拷贝     -----将对象完整的复制出来
#### 拷贝构造函数是在实际复制第二个字符串时为该字符串调用的构造函数。  当你试图创建一个新变量，并将其赋值给另一个与你实际创建的变量类型相同的变量时，你实际上是在复制该变量，因此调用了所谓的复制构造函数
