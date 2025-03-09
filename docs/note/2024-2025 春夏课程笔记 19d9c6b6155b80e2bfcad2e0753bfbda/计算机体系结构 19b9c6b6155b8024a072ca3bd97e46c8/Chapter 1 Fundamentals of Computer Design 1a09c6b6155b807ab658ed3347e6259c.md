# Chapter 1: Fundamentals of Computer Design

## 一、基本知识

1. **RISC：**Reduced Instruction Set Computer
2. **Moore’s Law（摩尔定律）**
    
    集成电路上可以容纳的晶体管数目在大约每经过18个月到24个月便会增加一倍。
    
3. **Amdahl‘s Law（阿姆达尔定律）**
    
    $Speedup\\=\frac{Execution\space Time_{old}}{Execution\space Time_{new}}\\=\frac 1{(1-Fraction_{enhanced})+\frac{Fraction_{enhanced}}{Speedup_{enhanced}}}$
    
    - 推论：如果只改善任务的一小部分，那么对整个任务的提升至多不超过（1 - 该部分在整个任务的占比）的倒数

## 二、计算机的类型

1. PMD：Personal Mobile Device
2. Desktop
3. Server
4. Cluster（集群）/ WSC（仓储式计算机）
5. Embedded（嵌入式）/ IoT Computer（物联网计算机）

## 三、并行 Parallelism

### 1. 应用并行和硬件并行

1. **Application Parallelism**
    - DLP（Data-Level Parallelism，数据级并行）
        - 对于同一项任务，同时处理多个数据（例如：排序、矩阵乘法的并行算法）
    - TLP（Task-Level Parallelism，任务级并行）
        - 使用同一组数据，同时处理多项任务（例如：将一组数据输入两个处理器，处理器 A 执行排序，处理器 B 执行求和运算）
2. **Hardware Parallelism**
    - ILP（Instruction-Level Parallelism，指令级并行）
        - Pipelining 技术：将一条指令分为多步，以使处理器能同时执行多条指令
        - 推测执行：通过预加载任务，避免执行时产生延迟（例如：分支预测）
    - Vector Architectures, GPU and Multimedia Instruction Sets
        - 利用数据级并行
        - 并行地将一个指令应用到一个数据集（例如： GPU 重复矩阵运算）
    - TLP（Thread-Level Parallelism，线程级并行）
        - 应用于允许并行线程之间交互的紧密耦合硬件模型中（例如多核处理器）
    - RLP（Request-Level Parallelism，请求级并行）
        - 利用编程人员或操作系统指定的大部分解耦任务之间的并行

### 2. 并行的 Flynn 分类

Flynn（人名）按照指令流、数据流的数目，将并行分为四类（**S**ingle/**M**ultiple **I**nstruction/**D**ata stream）：

1. **SISD（单指令流，单数据流）**
    - 单处理器（uniprocessor）
    - 利用指令级并行
2. **SIMD（单指令流，多数据流）**
    - 多个处理器使用不同的数据流执行相同的指令
    - 每个处理器都有数据存储器，但只有一个指令存储器和控制处理器
    - 利用指令级、数据级并行
3. **MISD（多指令流，单数据流）**
    - 无对应的商用处理器
4.  **MIMD（多指令流，多数据流）**
    - 利用指令级、数据级、任务级并行

## 四、计算机体系结构 Computer Architecture

### 1. 计算机体系结构的组成内容

1. Instruction Set Architecture（ISA，指令集架构）
2. Organization / Microarchitecture（组成 / 微架构）
3. Hardware（硬件）

### 2. 指令集架构（ISA）的七个维度

1. **Class of ISA**
    - 大多 ISA 具有通用寄存器架构（General-Purpose Register Architectures），即操作数（Operands）既可以是寄存器又可以是内存地址
    - ISA 的分类
        - Register-Memory ISA：很多指令都可以访问内存（例如：80x86）
        - Load-Store ISA：只有 load 和 store 指令可以访问内存（例如：RISC-V）
2. **Memory Addressing（内存地址）**
    - 所有 ISA 都采用字节地址（Byte addressing），但不一定要求地址对齐
    - 地址对齐（Address Alignment）的定义
        - 若对象的大小为 s 字节
        - 其内存地址为 A
        - 若 A mod s = 0，则该对象是地址对齐的
    - 访问一个没有地址对齐的对象，需要执行两次内存访问

![图：地址对齐的示例](Chapter%201%20Fundamentals%20of%20Computer%20Design%201a09c6b6155b807ab658ed3347e6259c/image.png)

图：地址对齐的示例

1. **Addressing Modes（寻址模式）**
2. **Types and sizes of operands（操作数的类型和大小）**
3. **Operations（操作）**
    - Data Transfer
    - Arithmetic / Logical
    - Control
    - Floating Point
4. **Control Flow Instructions（控制流指令）**
    - Conditional Branches
    - Unconditional Jumps
    - Procedure Calls
    - Returns
5. **Encoding an ISA（指令的编码）**
    - 分为定长（例如：RISC-V）和可变长（例如：80x86）

## 五、科技发展

### 1. 计算机的技术实现

1. 集成电路（Integrated Circuit Logic Technology）
2. 半导体 DRAM（Semiconductor DRAM）
3. 半导体闪存（Semiconductor Flash）
4. 磁盘（Magnetic Disk Technology）
5. 网络（Network Technology）

### 2. 带宽与延迟

1. **定义**
    - Bandwidth / Throughput（带宽）：在一定时间内进行的工作总量
    - Latency / Response Time（延迟）：同一项任务从开始到结束的用时长度
2. **晶体管（Transistor）和线路（Wire）的影响**
    - 特征尺寸（Feature Size）：晶体管或导线在 X 轴或 Y 轴方向的最小尺寸
    - 特征尺寸越小，线路变得更短，但是电阻和电容变得更糟，因此延迟会变得更长

### 3. 功耗与能耗

1. **定义**
    - 功率/功耗（Power）：单位时间的能耗（ 1 Watt = 1 J/s）
    - 能耗（Energy）：平均功率 × 运行时间
2. **动态能耗（Dynamic Energy）：**开关晶体管的能耗，是主要的耗能源
    
    ![image.png](Chapter%201%20Fundamentals%20of%20Computer%20Design%201a09c6b6155b807ab658ed3347e6259c/image%201.png)
    
3. **静态功耗（Static Power）**
    - 产生原因：晶体管在关闭状态下存在泄漏电流，易失性存储器（SRAM等）需要通电以维持存储的数据
    - 静态功耗与器件数目呈正比： $功耗_{静态}\propto 电流_{静态}\times 电压$
4. **分析**
    - 对于一项固定任务，降低时钟频率可以降低功率，但不会降低能耗（因为降低时钟频率会增大运行时间）
    - 减小电压可以显著降低功率和能耗
5. **提升能效表现的方法**
    - 以逸待劳：关闭非活动模块的时钟，以降低能耗和动态功耗
    - 动态电压—频率缩放（Dynamic Voltage-Frequency Scaling，DVFS）：在活跃程度较低的期间，降低时钟频率和电压
    - 为典型情景进行特别设计
    - 超频（Overclocking）：在较短的时间内，芯片以更高的时钟频率进行工作，直到其温度上升到一定值后恢复正常时钟频率
    - 竞相暂停（Race-to-halt）：由于处理器只是系统整体能耗中的一部分，所以如果使用一个速度较快但能效较低的处理器，从而更快地完成任务，并使系统的其他部分能够进入睡眠模式，可能有助于降低整体能耗

### 4. 集成电路的成本

1. 晶片（Dies）由晶圆（Wafer）切割而成
2. **计算集成电路的成本**
    
    ![image.png](Chapter%201%20Fundamentals%20of%20Computer%20Design%201a09c6b6155b807ab658ed3347e6259c/image%202.png)
    
    ![image.png](Chapter%201%20Fundamentals%20of%20Computer%20Design%201a09c6b6155b807ab658ed3347e6259c/image%203.png)
    
    ![image.png](Chapter%201%20Fundamentals%20of%20Computer%20Design%201a09c6b6155b807ab658ed3347e6259c/image%204.png)
    
    - N 表示加工 - 复杂度因子（Process-Complexity Factor），用于测量制造难度
    - 需考虑良率（Yield）的影响

## 六、可靠性 Dependability

### 1. 故障与恢复

- 基础设施供应商提供服务水平协议（Service Level Agreements，SLA）或服务水平目标（Service Level Objectives，SLO）来保证他们的网络或电力服务是可靠的。因此我们可以用 SLA 来判断系统处于运行还是停机状态。可以将服务状态分为：
    1. **服务实现**（Service Accomplishment）：按照 SLA 的说明提供服务
    2. **服务中断**（Service Interruption）：提供的协议与 SLA 说明的不同
- 状态 1 → 2 的转变称为**故障**（Failures），2 → 1 的转变称为**恢复**（Restorations）

### 2. 可靠性与可用性

1. **模块可靠性**（Module Reliability）：从一个参考的初始时刻开始，对连续的服务实现的衡量
    - 平均故障时间（Mean Time to Failure, MTTF）：它的倒数即为故障率，可用 FIT（Failure in Time）表示
    - 平均修复时间（Mean Time to Repair, MTTR）
    - 平均故障间隔时间（Mean Time Between Failures, MTBF) = MTTF + MTTR
2. **模块可用性**（Module Availability）：对实现和中断两种状态交替的服务实现的衡量，计算公式为：
    
    $$
    Availability=\frac{MTTF}{MTTF+MTTR}
    $$
    

### 3. Fault、Error、Failure

- Fault 是设计的瑕疵
- 当 Fault 发生时，它会产生一个或多个潜在的 Error
- 当 Error 实际影响交付的服务时，就会发生 Failure

> **示例：**
> 
> 
> 假设一个系统由以下器件组成：
> 
> - 10 个硬盘，每个硬盘的 MTTF 为 $10^6$ 小时
> - 1 个 ATA 控制器，MTTF 为 500000 小时
> - 1 个电源，MTTF 为 200000 小时
> 
> 求整个系统的 MTTF
> 
> **解：**
> 
> $总计故障率=10\times\frac1{10^6}+\frac1{500000}+\frac1{200000}\\MTTF=\frac1{总计故障率}$
> 

## 七、RAID & Stripe Data（分布式存储）

详见“计算机组成”笔记

## 八、性能的评估

### 1. Benchmarks

- **基准测试**（Benchmarks）：用于评估计算机性能的程序
- **基准测试套件**（Benchmark Suite）：一组基准测试应用
    - 其中一个最成功的标准基准测试套件是 [SPEC](https://www.spec.org/)（标准性能评估公司 , Standard Performance Evaluation Corporation）

不同计算机类型的基准测试：

- 台式机：
    - 处理器密集型（Processor-intensive)/ 图形密集型（Graphics-intensive）基准测试
    - 整数 / 浮点数基准测试
- 服务器：
    - 面向处理器吞吐量的基准测试
    - SPECrate：用于测量请求级并行
    - 关于 I/O：文件服务器基准测试（SPECSFS）、Java 服务器基准测试
    - 事务处理 (TP) 基准测试：测量系统处理由数据库访问和更新构成的事务的能力

### 2. 性能测试结果的分析与总结

1. SPECRatio：基准计算机的执行时间 / 被测计算机的执行时间，有以下等式成立：
    - 与基准计算机进行比较时：
    
     $SPEC\_Ratio=\frac{运行时间_{基准计算机}}{运行时间_{A计算机}}=\frac{Performance_{A计算机}}{Performance_{基准计算机}}$
    
    - 与另一条计算机进行比较时：
    
    $SPEC\_Ratio=\frac{运行时间{B计算机}}{运行时间_{A计算机}}=\frac{Performance_{A计算机}}{Performance_{B计算机}}$
    
2. 由于 SPECRatio 是比率而非绝对执行时间，因此计算平均值时应采用几何平均值（Geometric Mean），即：
    
    $几何平均=\sqrt[n]{\prod_{i=1}^n{sample_i}}$
    
    其中， $sample_i$ 表示第 i 个样本的 SPECRatio
    
    从而保证 A 与 B 的SPECRatio 的几何平均值之比，等于对 A 与 B 执行套件中所有基准测试所得性能比的几何平均值，而与基准计算机的选择无关