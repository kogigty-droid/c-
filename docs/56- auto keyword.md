# auto 关键字
### auto 使用场景1： 使用iterator的时候

```cpp
std::vector<std::string> strings;
strings.push_back("Apple");
strings.push_back("Orange");
for (std::vector<std::string>::iterator it = strings.begin(); //不使用auto
    it != strings.end(); it++)
{
    std::cout << *it << std::endl;
}
for (auto it = strings.begin(); it != strings.end(); it++) //使用auto
{
    std::cout << *it << std::endl;
}
```
### 使用场景2
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>

class Device{};

class DeviceManager
{
private:
    std::unordered_map<std::string, std::vector<Device *>> m_Devices;
public:
    const std::unordered_map<std::string, std::vector<Device *>> &GetDevices() const
    {
        return m_Devices;
    }
};

int main()
{
    DeviceManager dm;
    const std::unordered_map<std::string, std::vector<Device *>> &devices = dm.GetDevices();//不使用auto
    const auto& devices = dm.GetDevices(); //使用auto

    std::cin.get();
}
```

### 除此之外类型名过长的时候也可以使用using或typedef方法：
```cpp

**auto使用建议:**如果不是上面两种应用场景，请尽量不要使用auto！能不用，就不用！

using DeviceMap = std::unordered_map<std::string, std::vector<Device*>>;
typedef std::unordered_map<std::string, std::vector<Device*>> DeviceMap;

const DeviceMap& devices = dm.GetDevices();
```

**auto使用建议**: 如果不是上面两种应用场景，请尽量不要使用auto！能不用，就不用！

