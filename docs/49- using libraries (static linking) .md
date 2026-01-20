# using libraries (static linking)    使用库（静态链接）

### 二进制文件进行链接  GLFW库 ，而不是获取实际依赖库的源代码并自己进行编译  

### 静态链接与动态链接区别                ----静态相对来说更好

<img width="1149" height="301" alt="image" src="https://github.com/user-attachments/assets/f2155e8b-cc0b-4403-b8a8-e5ee38bca3ca" />

<img width="698" height="75" alt="image" src="https://github.com/user-attachments/assets/cc6e6473-0a4e-4151-9903-3d7025f0cd29" />

#### 静态链接意味着这个库会被放到你的可执行文件中，他在你的exe文件中，或其他操作系统下的可执行文件；库文件是否诶编译到exe文件中或链接到exe文件中

<img width="1155" height="265" alt="image" src="https://github.com/user-attachments/assets/b9ec021e-909e-4943-8463-00665a5f1706" />

#### 动态链接库是在运行时被链接的，所以你仍然有一些链接，你可以选择在程序运行时，装载动态链接库； 只是一个单独的文件，但你运行时，需要把它放在哪你的exe文件旁边或某个地方，然后你的exe文件可以加载他

<img width="1170" height="260" alt="image" src="https://github.com/user-attachments/assets/e9e0f709-d960-47bd-9f0b-3f406a32da10" />




