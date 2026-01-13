# const 关键字

##### 绕开const的方法： 强制转换：

```cpp
  const int Age =90;
  int* a = new int;
  *a = 2;    //1.改变指针指向的内存内容
  a = &Age //error!
  a =(int*)&Age //ok   //改变指针指向的内存地址   把Age的地址取出来给到a
```
<details>
<summary>没有const的声明</summary>

```cpp
int main ()
{
    const int MAX_AGE = 90;  //常量  不可修改
    int* a = new int;  //在堆上创建一个整型，这个声明没有做const  因此可以做两件事
    *a = 2;      //1)解引用a 并赋值为2
    a = (int*)&MAX_AGE;  //2)重新分配指针（改变指针a指向的内存地址）  让a指向另一个地址    不建议强制转换
    std::cout << *a << std::endl;

}
```
</details>
