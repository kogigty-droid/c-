# smart pointer 智能指针 std--unique_ptr  std--shared_ptr  std--weak_ptr
### 智能指针就是说当你调用new分配内存的时候，你不用自己去调用。实际上在很多使用智能指针的情况下，甚至不用去调用new。
#### 智能指针其实就是对原始指针的包装。当你创建一个智能指针，他会调用new 为你分配内存，然后基于你使用的智能指针，分配的内存会在某一时刻自动释放。
### 最简单的智能指针 unique_ptr 作用域指针：当这个指针超出作用域时，他就会被销毁，就会调用delete。
#### unique_ptr必须是unique的，不能copy一个unique_ptr,如果copy的话，他们会指向同一个内存地址，当你其中一个unique_ptr指针die的时候，他就是释放那块内存，指向相同内存地址的第二个unique_ptr就会指向已经被释放的内存
### 要使用这些智能指针，需要先引入<memory>头文件 

#### 注意：隐式转换 std::unique_ptr<Entity> entity= new Entity()；不能使用隐式转换原因： new Entity()返回的是裸指针Entity*，而左边的是智能指针对象std::unique_ptr<Entity> entity； =：是在告诉编译器：“请帮我隐式地把右边的这个裸指针（内存地址），包装成左边的智能指针对象（类对象）。然而，std::unique_ptr 的构造函数中有explicit 关键字，说明这个构造函数只能显式调用，不能用于隐式转换。      很显然 类对象≠指针

### std::unique_ptr<Entity> 是 C++ 标准库定义的一个模板类（Template Class）。虽然我们叫它“智能指针”，但它不是指针，它是一个对象

#### std::unique_ptr<Entity>这个标准类里面就是要求传入一个指针

<img width="1055" height="453" alt="image" src="https://github.com/user-attachments/assets/66e9bdfa-d8f6-4154-b4c0-f78070f0c6d9" />

<img width="1200" height="678" alt="image" src="https://github.com/user-attachments/assets/61a211cf-f9a3-4f6c-904a-52e6acf4d81b" />



