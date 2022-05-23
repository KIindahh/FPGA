[TOC]

# 1.Verilog HDL语法

## 1.1基本概念



### 1.1.1基本格式

```verilog
module 模块名（端口名1 端口名2 端口名3 ...）;
    端口类型说明（input，output,inout）;
    参数定义（可选）;
    数据类型定义（wire，reg等）;
    实例化底层模块和基本门级元件;
    连续赋值语句（assign）;
    过程块结构（initial 和 always）;
	行为描述语句；
endmodule
```

eg：

```verilog
module example{
    input    wire  //输入信号
    inout    wire  	//输入输出信号
    output	 wire   	//输出信号
}
	//线网型变量
    wire [0:0]	flag;
	//寄存器型变量
    reg	 [7:0]	cnt;
    
    //全局变量
    parameter CNT_MAX = 100;
    //局部变量
    localparam CNT_MAX = 100;
    
    //
    example
    #(
    
    )//顶层模块
    example_inst
    (
    
    )
    //always模块
    //重复执行
    always@()//当敏感事件（电平跳变等）发生时，执行语句
        begin/for
        end/join
    //intial模块
    //只执行一次
    intial
    	begin/for
    	end/join
```





### 1.1.2注释、间隔符和标识符

1. 注释

```verilog
①//单行注释
②/*
多行注释
Verilog HDL定义了一系列保留字（关键词，不能当成标识符）
保留字的拼写为小写字母
*/
```

2. 间隔符

```verilog
空格 (\b)、tab(\t)
换行符 (\n)
```





### 1.1.3数值和字符串

1. 数值

   ```verilog
   0：逻辑0或假状态
   1：逻辑1或真状态
   x：未知状态
   z:高阻态，物驱动 //在们输入时，常解释成“x”
   //以上四种值已内置
   ```

   

2. ### 常量类型

   ```verilog
   [位宽]‘[进制][数值]
   [B][O][D][H]
   //阻塞语句
   顺序执行
   //非阻塞语句
   并行
   ```

### 1.1.4系统函数

# 2.组合逻辑

## 2.1概念

> 组合逻辑：只和当前信号（该时刻输入）有关，与电路原本状态无关。一般使用@always和assign两种语法。

```verilog
//实例化
decoder decoder_inst
(
    .in_1(in_1),//括号里的是仿真文件生成的，两个相连
    .in_2(in_2),
    ....
)
```



## 2.2多路选择器

> 概念：利用sel来选择输出哪条路

eg:

```verilog
module mix_2
    (
        input wire int_1,
        input wire int_2,
        input wire sel,
        output reg out
    
    );
    always@(*)//赋值
        begin
            if(sel == 1'b0)
                out = int_1;
            else if (sel == 1'b0)
                out = int_2;
        end //利用sel来选择输出是int1还是int2的电平 
    
```

## 2.3译码器

> 概念：把某些二进制代码所代表的特定含义翻译出来（把机器看得懂——>人看得懂）
>
> 分类：①变量译码 ②显示译码

3——8译码器（？真值表怎么得到的？）

![image-20220513135505034](C:\Users\kk\AppData\Roaming\Typora\typora-user-images\image-20220513135505034.png)

eg:

```verilog
module decoder
    
   
endmodule
```

## 2.3半加器

> 二进制相加，但没传入进位符

## 2.4latch

> 概念：将信号暂存以维持某电平。
>
> 造成latch的情况：
>
> 1）逻辑语句（if—esle/case）不完整
>
> 2）输出变量赋值给自己

# 3.时序逻辑

## 3.1寄存器

> 作用：存储
>
> 种类：①同步复位的D触发器：触发需要等待工作时钟上升沿（下降沿）触发②异步复位的D触发器
>
> 特点：”延一拍“

[example](E:\course\fpga\code\filp_flop)



## 3.2阻塞值与非阻塞值

> **注意**：非阻塞操作只能用于对寄存器类型变量进行赋值，因此只能用于“initial”和“always”块中，不允许用于连续赋值“assign”。

**规范：**

（1）时序逻辑采用非阻塞赋值

避免阻塞赋值时出现得不必要顺序，准备好赋下一状态的值。

（2）用always模块编写组合逻辑时用阻塞赋值

由于有敏感列表（电平触发），所以用阻塞赋值又快又好，不用等待

（3）在同一个always块中不要既要用非阻塞赋值又用阻塞方式赋值 



## 3.3计数器

> 计数来源：外部晶振产生的时钟
>
> 作用：对脉冲的个数经行计数，实现测量、计数和控制，分频的功能
>
> 掌握：何时计数，何时清零（？）

[example](E:\course\fpga\code\counter)

## 3.4分频器



## 3.5按键消抖

> 解决方案：
>
> ①利用计数器20ms（999_999）内判断电平有无变化②判断20ms时电平

容易出现的问题：

①由于低电平时间过长，计数器重复计数，输出多个脉冲信号（解决方案：计数器清零条件：20ms+key_in为高电平时）

②脉冲信号变长电平（解决方案：计数器计数到999_998时key_flag变换）



# 4.VGA

## 4.1显示原理

```
在行、场同步信号的同步作用下从左上角第一个像素点向右扫描，扫描标第一行行尾转移到第二行行首，重复，并给每一个像素点赋值，利用视觉暂留现象在屏幕上显示图片。
```

## 4.2时序标准

4.2.1行同步时序标准

> ync（同步）、Back Porch（后沿）、Left Border（左边框）、“Addressable” Video（有效图像）、Right Border（右边框）、Front Porch（前沿），这6部分的基本单位是pixel（像素），即一个像素时钟周期。

4.2.2场同步时序标准

> Sync（同步）、Back Porch（后沿）、Top Border（上边框）、“Addressable” Video（有效图像）、Bottom Border（底边框）、Front Porch（前沿），与行同步信号不同的是，这6部分的基本单位是line（行），即一个完整的行扫描周期。

**注意**：Video图像信息只有在“Addressable” Video（有效图像）阶段，图像信息有效，其他阶段图像信息无效。

## 4.3相关模式以及参数

![image-20220523203146237](C:\Users\kk\AppData\Roaming\Typora\typora-user-images\image-20220523203146237.png)

eg:

```verilog
//显示模式
640×480@60
//每一行有640个像素点，共480行；@60刷新频率，指每秒刷新图像60次

//时钟（MHz）计算方法：时钟频率 = 行扫描周期*场扫描周期*刷新频率 
25.175
```

## 4.4模块

4.4.1模块图

<img src="C:\Users\kk\AppData\Roaming\Typora\typora-user-images\image-20220523205812324.png" alt="image-20220523205812324" style="zoom: 25%;" />



4.4.2example

[VGA:显示彩条](E:\course\fpga\VGA)

