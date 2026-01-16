# smart pointer 智能指针 std--unique_ptr  std--shared_ptr  std--weak_ptr
### 智能指针就是说当你调用new分配内存的时候，你不用自己去调用。实际上在很多使用智能指针的情况下，甚至不用去调用new。
#### 智能指针其实就是对原始指针的包装。当你创建一个智能指针，他会调用new 为你分配内存，然后基于你使用的智能指针，分配的内存会在某一时刻自动释放。
### 最简单的智能指针 unique_ptr 作用域指针：当这个指针超出作用域时，他就会被销毁，就会调用delete。
#### unique_ptr必须是unique的，不能copy一个unique_ptr,如果copy的话，他们会指向同一个内存地址，当你其中一个unique_ptr指针die的时候，他就是释放那块内存，指向相同内存地址的第二个unique_ptr就会指向已经被释放的内存
### 要使用这些智能指针，需要先引入<memory>头文件
