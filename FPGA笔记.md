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