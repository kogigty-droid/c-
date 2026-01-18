# dynamic array (vector)    本质是个动态数组  但不是矢量

### 一开始不知道数组中到底要多少元素     比如：足够容纳10个元素的内存，当你超过这个大小的时候，他会在内存中创建比第一个更大的新数组，把所有东西赋复制到这里，然后删除旧的那个

#### vertex对象，那么内存分配是一条线上的  但是调整vector重新分配和复制的过程比较缓慢；指针不同，实际的内存保持不变，你只是正确的保存了指向内存的指针，所以实际的内存保持不变，到了调整大小的时候，他只是副本，即整数，只是实际数据的内存地址，而数据仍然被储存。  
###  尽量选择对象，而不是指针！

#### 一些问题

<img width="1080" height="426" alt="image" src="https://github.com/user-attachments/assets/7139dbce-42b4-4c7d-b619-d8302e60308a" />

<img width="1118" height="618" alt="image" src="https://github.com/user-attachments/assets/b2d74bb0-8802-4a95-9b51-7ae98d58015c" />

#### 简化对数组、Vector等容器的遍历

<img width="979" height="450" alt="image" src="https://github.com/user-attachments/assets/b8eaf34f-6a02-44e7-a906-5a161453172a" />

#### 将vertex传递给函数或类或其他东西时，要确保使用的是引用传递他们

<details>
<summary>动态数组</summary>

```cpp
#include<iostream>
#include <string>
#include<vector>

struct Vertex
{
    float x,y,z;

};

std::ostream& operator<< (std::ostream& stream, const Vertex& vertex) 
{
    stream << vertex.x << "," << vertex.y << "," << vertex.z;
    return stream;
}

void Function(const std::vector<Vertex>& vertices)
{

}

int main()
{
    std::vector<Vertex> vertices;  //动态数组(容器---里面有很多个Vertex)    vertex对象，那么内存分配是一条线上的  但是重新分配和复制的过程比较缓慢
    vertices.push_back({1,2,3});   //往容器的末尾“追加（Append）”新的元素
    vertices.push_back({4,5,6});

    Function(vertices);

    for (int i = 0; i < vertices.size(); i++)
        std::cout << vertices[i] << std::endl; 
    
    //单独移除某个vertex
    vertices.erase(vertices.begin() + 1);     //假如删除第二个元素
            
    // for(Vertex v : vertices)
    //     std::cout << v << std::endl;      //这里实际上是将每个v复制到for循环中，为了避免复制 ，用引 只要有&就不会复制数据
    
    for(const Vertex& v : vertices)
        std::cout << v << std::endl;

    vertices.clear();    //清除vertex列表    数组大小会被置0
     
    

    std::cin.get();

}

```
</details>
