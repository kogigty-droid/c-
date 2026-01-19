# optimizing the usage of std -- vector   更优的方式使用vector类

### 传入对象

```cpp
std::vector<Vertex> vertices;       //vector 的内存必须是连续的    位置不够则要重新申请一块新的，再把之前里面旧的复制到新的     每次申请地址成倍   1->2->4->8.... 
vertices.push_back({1,2,3});        //需要先把Vertex(1,2,3)复制到vector容器里面
vertices.push_back({4,5,6});
vertices.push_back({7,8,9});
```

### 传入参数列表

```cpp
std::vector<Vertex> vertices;       //vector 的内存必须是连续的    位置不够则要重新申请一块新的，再把之前里面旧的复制到新的     每次申请地址成倍   1->2->4->8....
vertices.reserve(3);                 //告诉vector我们要放三个进去  （减少copy）
 //利用vertices.emplace_back(1,2,3);   只传递构造函数的参数列表
vertices.emplace_back(1,2,3);    //只传递构造函数的参数列表
vertices.emplace_back(4,5,6); 
vertices.emplace_back(7,8,9); 
```

<details>
<summary>优化</summary>

```cpp
#include<iostream>
#include<string>
#include<vector>

struct Vertex
{
    float x,y,z;

    Vertex(float x, float y, float z)
        :x(x),y(y),z(z)
    {
    }
};

int main()
{
    std::vector<Vertex> vertices;       //vector 的内存必须是连续的    位置不够则要重新申请一块新的，再把之前里面旧的复制到新的     每次申请地址成倍   1->2->4->8....
    vertices.reserve(3);                 //告诉vector我们要放三个进去  （减少copy）
    // vertices.push_back(Vertex(1,2,3));   //需要先把Vertex(1,2,3)复制到vector容器里面
    // vertices.push_back(Vertex(4,5,6));
    // vertices.push_back(Vertex(7,8,9));

    //利用vertices.emplace_back(1,2,3);   只传递构造函数的参数列表
    vertices.emplace_back(1,2,3);    //只传递构造函数的参数列表
    vertices.emplace_back(4,5,6); 
    vertices.emplace_back(7,8,9); 

}
```
</details>
