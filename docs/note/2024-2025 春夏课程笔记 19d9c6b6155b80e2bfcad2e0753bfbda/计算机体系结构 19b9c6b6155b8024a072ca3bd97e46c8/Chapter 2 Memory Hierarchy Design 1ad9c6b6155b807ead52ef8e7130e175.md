# Chapter 2: Memory Hierarchy Design

## 一、概述

### 1. 存储层次示意图

![image.png](Chapter%202%20Memory%20Hierarchy%20Design%201ad9c6b6155b807ead52ef8e7130e175/image.png)

### 2. **评估标准**

1. **Bandwidth（带宽）**
2. **Latency（延迟）：**分为获取时间（Access Time）和循环时间（Cycle Time）
    - 获取时间：发送读请求到字到达需要的时间
    - 循环时间：不相关的内存请求需要的最小时间，即获取开始和下一次获取开始之间的最小时间

### 3. 硬件原理

1. **SRAM**
    - 全称：Static Random Access Memory
    - 每个 bit 使用六个晶体管保存，以防止信息在读取时受到干扰
    - 不需要刷新，Access Time 接近于 Cycle Time
2. **DRAM**
    - 全称：Dynamic Random Access Memory
    - 每个 bit 使用单个晶体管保存
    - 读操作会破坏信息
    - 需要周期性刷新
    - Cycle Time > Access Time

### 4. Cache 的组织形式

1. **Direct Mapped**
    
    ![image.png](Chapter%202%20Memory%20Hierarchy%20Design%201ad9c6b6155b807ead52ef8e7130e175/image%201.png)
    
2. **Set Associated**
    
    ![image.png](Chapter%202%20Memory%20Hierarchy%20Design%201ad9c6b6155b807ead52ef8e7130e175/image%202.png)
    
3. **Fully Associated**
    
    ![image.png](Chapter%202%20Memory%20Hierarchy%20Design%201ad9c6b6155b807ead52ef8e7130e175/image%203.png)