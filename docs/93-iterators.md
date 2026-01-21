# iterators   迭代器---本质上是一种迭代元素集合的方法

## 迭代器分类：
#### 迭代器 iterator  (只有这个是用来迭代值的)  反向迭代器 reverse_iterator 常量迭代器 const_iterator  常量反向迭代器 const_reserve_iterator


## 键值对           ---由key找到value
<img width="920" height="350" alt="image" src="https://github.com/user-attachments/assets/8489d4b7-371d-4898-ba60-f74ef81ddb51" />


```cpp
#include<iostream>
#include<vector>
#include<unordered_map>

int main()
{
    std::vector<int> values = {1,2,3,4,5};    

    for (int i = 0;i < values.size();i ++)     //较为麻烦的循环
    {
        std::cout << values[i] <<std::endl;
    }

    for (int value : values)    //简洁代码  
    {
        std::cout << value << std::endl;
    }

    //迭代器
    for(std::vector<int>::iterator it = values.begin();   
        it != values.end(); it++)          //迭代器不等于这个集合的末尾就不终止这个循环
    {
        std::cout << *it << std::endl;
    }
    
    using ScoreMap = std::unordered_map<std::string,int>;
    ScoreMap map = {};
    map["Cherno"] = 5;
    map["Che"] = 2;

    for(ScoreMap::const_iterator it = map.begin(); it != map.end(); it++)
    {
        auto& key = it->first;    //键     it是一个指针
        auto& value = it->second;  //值
        std::cout << key << " = " << value << std::endl;
    }

    for(auto kv:map) //简洁的循环写法
    {
        auto& key = kv.first;    //键    kv是一个对象 所以用. 就可以访问 
        auto& value = kv.second;  //值
        std::cout << key << " = " << value << std::endl;
    }


    std::cin.get();
}

```
