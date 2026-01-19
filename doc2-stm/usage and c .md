
### STM32/GD32  开发流程：编辑、编译、链接、下载。  
MDK中集成了编辑器、编译器和链接器，使用MDK和开发板可以完成增高开发流程。
集成开发环境 ---像MDK这种集成了各种开发工具的软件

#### 变量作用：当系统执行到变量的定义语句时，系统将会为变量分配存储空间分配存储空间的大小由定义变量时的数据类型决定

<img width="1268" height="600" alt="image" src="https://github.com/user-attachments/assets/c013ce95-e107-481e-8355-577f7a909948" />

<img width="1124" height="289" alt="image" src="https://github.com/user-attachments/assets/155f50b5-e950-4463-a470-0c348e9806ba" />

### 按位与或
<img width="884" height="340" alt="image" src="https://github.com/user-attachments/assets/cfd8bbdf-cf2d-43d3-86ea-c87245f953c8" />

### 按位异或   ----当且仅当 两个不同时 才为真（1）

<img width="698" height="305" alt="image" src="https://github.com/user-attachments/assets/3f998dcc-8e3d-4fb3-a66f-72c455869272" />

### 左移，右移运算符

<img width="830" height="291" alt="image" src="https://github.com/user-attachments/assets/54f34e58-a2d9-4e5f-876b-a83790615d63" />

### 条件语句的嵌套
<img width="830" height="291" alt="image" src="https://github.com/user-attachments/assets/2ef8d844-9a66-478d-aba2-26ddcadeaf47" />

<details>
<summary>条件语句嵌套</summary>

```c
if(score > 90)
  printf("A\r\n");
else if(score > 80)
        printf("B\r\n");
     else if(score > 70)
             printf("C\r\n");
          else if(score > 60)
                  printf("D\r\n");
               else 
                 printf("E\r\n");
```
</details>

### 开关语句

<img width="775" height="234" alt="image" src="https://github.com/user-attachments/assets/8e77edb2-f594-4191-9a28-95b053e2607d" />

<img width="830" height="291" alt="image" src="https://github.com/user-attachments/assets/2ef8d844-9a66-478d-aba2-26ddcadeaf47" />

<details>
<summary>条件语句嵌套</summary>

```c
temp = score/10；

switch (temp)
{
  case 9: printf("A\r\n");break;
  case 8: printf("B\r\n");break;
  case 7: printf("C\r\n");break;
  case 6: printf("D\r\n");break;
  default: printf("你考的太烂了")；
  
}

```
</details>

<img width="1071" height="220" alt="image" src="https://github.com/user-attachments/assets/e6551e07-1ec1-4726-8ef8-f1808caf9a78" />

### 1.19
#### 1.给寄存器某个位赋值

<img width="1200" height="579" alt="image" src="https://github.com/user-attachments/assets/2cc06ccb-5019-44a3-8005-cd88e831fac7" />

#### 2.宏定义        ----预处理
#### 可以提高效率，易改性，可读性 核心是 替换

<img width="978" height="560" alt="image" src="https://github.com/user-attachments/assets/23fb1de2-0e31-4f82-9955-ae09dc2a5167" />

<img width="1274" height="550" alt="image" src="https://github.com/user-attachments/assets/a1e6a7c4-9c07-4c40-be44-dc33d78e9a39" />

#### 条件编译

<img width="1118" height="589" alt="image" src="https://github.com/user-attachments/assets/4e99c1c3-7fd2-4039-8206-446e2aaf5232" />

<img width="1088" height="510" alt="image" src="https://github.com/user-attachments/assets/cd55aef3-5aa1-4936-ae05-e2f912dce442" />

<img width="1130" height="469" alt="image" src="https://github.com/user-attachments/assets/d2eb8138-a81e-4c91-8f87-8ca5ad886003" />

#### 类型别名

<img width="1063" height="511" alt="image" src="https://github.com/user-attachments/assets/4843b017-3589-49ac-9e71-9abff7444145" />

<img width="1039" height="590" alt="image" src="https://github.com/user-attachments/assets/ea31806b-d061-498f-8455-b3865c85e651" />

<img width="1045" height="599" alt="image" src="https://github.com/user-attachments/assets/c70a1ecf-0119-4a6a-9147-c797659705ee" />

<img width="1179" height="471" alt="image" src="https://github.com/user-attachments/assets/5c7a7e0c-bd92-4fff-a0ea-f43d1f606e9f" />

<img width="1249" height="588" alt="image" src="https://github.com/user-attachments/assets/d3f6541e-3b99-44ea-baa0-3f230d5e5612" />

<img width="1069" height="514" alt="image" src="https://github.com/user-attachments/assets/c0169aae-0f3f-485c-a39b-ef28398e7f32" />

<img width="1073" height="591" alt="image" src="https://github.com/user-attachments/assets/4a0f88cc-9bdd-491a-93b0-e8d3a8325257" />



