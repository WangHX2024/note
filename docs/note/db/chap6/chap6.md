# Chapter 6: Relational Database Design

## 一、第一范式 First Normal Form

1. 如果域（Domain）是不可分的，则称域是原子（Atomic）的
2. 如果关系范式中的所有域都是原子的，则称该关系范式满足第一范式（1NF）
3. 一般要求关系型数据库中的所有关系都满足第一范式
    
    !!! example

        > **示例：**不满足第一范式的关系设计
        > 
        > - 复合属性：可以进一步分解为更小组件的属性
        > - 多值属性：允许存放多个值的属性
        > - 复杂数据类型：在属性中存放对象
        >     
        >     ```cpp
        >     学生ID| 姓名          | 课程
        >     1     | Tim,Cook     | 数学,物理
        >     2     | Steve,Jobs   | 化学
        >     
        >     // 姓名可以继续分为姓和名，故为复合属性
        >     // 课程允许存放多个值，故为多值属性
        >     // 它们都不满足第一范式
        >     ```
        >     

4. 将不满足第一范式的关系转化为第一范式
    - 对于复合属性，使用多个属性进行表示
    - 对于多值属性，使用多个属性或者一张单独的表进行表示

## 二、函数依赖 Functional Dependencies（FDs）

### 1. 函数依赖的概念

1. 定义
    - 令 $R$ 是关系范式， $\alpha$、 $\beta$ 是 $R$ 上的属性集
    - 函数依赖关系 $\alpha \rightarrow \beta$ 成立，当且仅当对任何合法的关系 $r(R)$ ，给出 $\alpha$ 的值能唯一确定 $\beta$ 的值
    
    !!! example

        > **示例：**
        > 
        > 
        > 在下图的关系中， $A\rightarrow B$ 不成立， $B\rightarrow A$ 成立
        > 
        > ![image.png](image.png)
        > 

2. 函数依赖与键（Key）的关系
    - $K$ 是 $R$ 的超键，当且仅当 $K\rightarrow R$
    - $K$ 是 $R$ 的候选键，当且仅当 $K\rightarrow R$ 且不存在 $K$ 的真子集 $\alpha$，使其满足 $\alpha \rightarrow R$
3. 平凡的函数依赖
    - 一个函数依赖是平凡的（trivial），若它对所有的关系范式都成立
    - 若 $\beta \subseteq \alpha$，则函数依赖 $\alpha \rightarrow \beta$ 是平凡的，否则则不是平凡的
    
    !!! example

        > **示例：**
        > 
        > $A\rightarrow A$、 $AB\rightarrow A$ 都是平凡的函数依赖
        > 

### 2. 函数依赖集的闭包 Closure of a Set of Functional Dependencies

1. 定义：由函数依赖集 $F$ 可以逻辑推导出的所有函数依赖关系组成的集合 $F^+$ 称为函数依赖集 $F$ 的闭包；函数依赖集与其闭包是等价关系
    
    !!! example

        > **示例：**
        > 
        > 
        > ![image.png](image%201.png)
        > 

2. Armstrong’s Axioms
    
    以下三条定律为基本定律：
    
    - 自反律（Reflexivity）：若 $\beta \subseteq \alpha$，则 $\alpha \rightarrow \beta$
    - 增补律（Argumentation）：若 $\alpha \rightarrow \beta$，则 $\gamma \alpha \rightarrow \gamma \beta$， $\gamma \alpha \rightarrow \beta$
    - 传递律（Transitivity）：若 $\alpha \rightarrow \beta$， $\beta \rightarrow \gamma$，则 $\alpha \rightarrow \gamma$
    
    以下三条定律为导出定律，它们可以由基本定律导出：
    
    - 合并律（Union）： 若 $\alpha \rightarrow \beta$， $\alpha \rightarrow \gamma$，则 $\alpha \rightarrow \beta \gamma$
    - 分解律（Decomposition）：若 $\alpha \rightarrow \beta \gamma$，则 $\alpha \rightarrow \beta$， $\alpha \rightarrow \gamma$
    - 伪传递律（Pseudotranstivity）：若 $\alpha \rightarrow \beta$， $\gamma \beta \rightarrow \delta$，则 $\alpha \gamma \rightarrow \delta$
    
    !!! example

        > **示例：**
        > 
        > 
        > ![image.png](image%202.png)
        > 

3. 求函数依赖集的闭包的算法
    
    ![image.png](image%203.png)
    
4. 对于 $n$ 个属性的关系范式，其函数依赖集的闭包最多可能有 $2^n\times 2^n$ 个元素

### 3. 属性集的闭包 Closure of Attribute Sets

1. 定义：在函数依赖集 $F$ 下，由属性集 $a$ 能够决定的所有属性的集合 $a^+$称为属性集 $a$ 的闭包
2. 求属性集的闭包的算法
    
    ![image.png](image%204.png)
    
3. 使用属性集的闭包检查超键
    - 原理：若 $a$ 是超键，则 $R \subseteq a^+$
    - 方法：求 $a$ 的闭包 $a^+$，若 $R$ 的所有属性都包含于 $a^+$，则 $a$ 是超键
    
    !!! note

        **可以使用画图的方法寻找超键 / 候选键**
        
        - 在左图所示的函数依赖关系中，AG 是候选键，而 AB 不是
        - 在右图所示的函数依赖关系中，AC、BC 是候选键
        
        ![image.png](image%205.png)
        
        **使用画图寻找超键 / 候选键时，一定要小心遗漏**
        
        !!! example

            > **示例：**
            > 
            > 
            > $R=(A, B, C, D ,E)$
            > 
            > $F=\set{A\rightarrow B, BC\rightarrow D, D\rightarrow A}$
            > 
            > 使用画图的方法寻找候选键时，一定不要遗漏 $E$，正确答案为 $ACE$， $BCE$， $CDE$
            > 
            > ![image.png](image%206.png)
            > 
    

### 4. 正则覆盖 Canonical Cover

1. 定义：函数依赖集 $F$ 中可能存在冗余项，将 $F$ 中的冗余完全清除后，得到的函数依赖集称为正则覆盖，记为 $F_c$；函数依赖集与其正则覆盖是等价关系
2. 正则覆盖的特点
    - 正则覆盖中不存在无关的函数依赖和无关属性（Extraneous Attribute）
    
    !!! example

        > **示例：**无关属性可以出现在函数依赖项的箭头左侧或右侧
        > 
        > 
        > ![image.png](image%207.png)
        > 

    - 正则覆盖中，每一项的箭头左侧的属性集是唯一的
    
    !!! example

        > **示例：**
        > 
        > - 若函数依赖集中同时存在 $\alpha_1 \rightarrow \beta_1$、 $\alpha_1 \rightarrow \beta_2$，则它一定不是正则覆盖
        > - 可将其简化为 $\alpha_1 \rightarrow \beta_1 \beta_2$

3. 无关属性的定义和检测
    
    ![image.png](image%208.png)
    
4. 求正则覆盖的算法
    
    ![image.png](image%209.png)
    
    !!! example

        > **示例：**
        > 
        > 
        > ![image.png](image%2010.png)
        > 

## 三、分解 Decomposition

!!! note

    如果关系范式 $R$ 是 “不好的”，则将它分解（decompose）为一组关系 $\set {R_1, R_2, … , R_n}$，并满足以下要求：

    - 分解过程不能丢失任何属性（最基本的要求）
    - 分解过程是无损连接分解
    - 分解过程是依赖保持的
    - 分解得到的每个关系 $R_i$ 都是 “好的”，即满足 BCNF 或 3NF

### 1. 无损连接分解 Lossless-join Decomposition

1. 定义：将关系范式 $R$ 分解为 $R_1$、 $R_2$，若对任何可能的关系 $r$，有
    
     $r=\Pi_{R_1}(r)\bowtie \Pi_{R_2}(r)$
    
    则称该分解为无损连接分解
    
2. 测试分解是否是无损连接分解
    
    将关系范式 $R$ 分解为 $R_1$、 $R_2$ 为无损连接分解，当且仅当下面至少一个式子在 $F^+$ 上成立
    
    （即：分解后的两个子范式的公共属性必须是 $R_1$ 或 $R_2$ 的键）
    
    - $\set{R_1\cap R_2}\rightarrow R_1$
    - $\set{R_1\cap R_2}\rightarrow R_2$

!!! example

    > **示例：**在下图所示的分解中，无法通过对分解后的两张表进行自然连接得到分解前的表，因此不是无损连接分解
    > 
    > 
    > ![image.png](image%2011.png)
    > 

### 2. 依赖保持 Dependency Preservation

1. 含义：分解后的关系范式仍然能够保持原关系范式的所有函数依赖关系
2. 意义：在对函数依赖关系进行检查时，无需进行表的连接（join）就可以对函数依赖关系进行验证，从而提高检查效率
3. 定义
    - 设分解后的关系范式 $R_i$ 具有函数依赖 $F_i$，其中 $F_i\subseteq F^+$，且 $F_i$ 只包含 $R_i$ 中的属性
    - 若 $(F_1, F_2, … ,F_n)^+=F^+$，则该分解是依赖保持的
4. 测试分解是否依赖保持的算法
    
    ![image.png](image%2012.png)
    
!!! example    

    > **示例：**
    > 
    > 
    > 将 $R=(A, B, C)$， $F=\set{A\rightarrow B, B\rightarrow C}$ 进行分解
    > 
    > ![image.png](image%2013.png)
    > 

## 四、Boyce-Codd Normal Form

### 1. 定义

函数依赖集 $F$ 下的关系范式 $R$ 满足 BCNF，若对于 $F^+$ 中的每一个函数依赖 $\alpha\rightarrow\beta$，以下两条至少有一条成立：

- $\alpha\rightarrow\beta$ 是平凡的（即 $\beta\subseteq\alpha$）
- $\alpha$ 是 $R$ 的超键（即 $R\subseteq \alpha^+$）

!!! note

    由上述定义，只有两个属性的关系范式一定满足 BCNF

!!! example

    > **示例：**
    > 
    > 
    > 考虑 $R=(A, B, C)$， $F=\set{A\rightarrow B, B\rightarrow C}$ 
    > 
    > - 考虑 $B\rightarrow C$，由于 $B$ 不是 $R$ 的超键，所以 $R$ 不满足 BCNF

### 2. Testing For BCNF

- 为检测关系范式 $R$ 是否满足 BCNF，不必如定义所述对 $F^+$ 中每一个 $\alpha\rightarrow\beta$ 进行检验，只需对 $F$ 中的每一个 $\alpha\rightarrow\beta$ 检验即可；这是因为 $F^+$ 是由 $F$ 根据 Armstrong 的三条基本定理推导出的，而任何定理都不会使 $\alpha$ 变小
- 然而，若要检测 $R$ 经分解得到的关系范式 $R_i$ 是否满足 BCNF，则必须如定义所述对 $F^+$ 中每一个 $\alpha\rightarrow\beta$ 进行检验

!!! example

    > **示例：**
    > 
    > 
    > ![image.png](image%2014.png)
    > 

### 3. BCNF Decomposition Algorithm

任何关系都可以无损连接分解为 BCNF，但可能破坏依赖保持

![image.png](image%2015.png)

!!! example

    > **示例：**
    > 
    > 
    > ![image.png](image%2016.png)
    > 

### 4. BCNF 破坏依赖保持的问题

任何关系都可以无损连接分解为 BCNF，但可能破坏依赖保持

!!! example

    > **示例：**
    > 
    > 
    > 考虑 $R=(J, K, L)$， $F=\set{JK\rightarrow L, L\rightarrow K}$
    > 
    > - 考虑 $L\rightarrow K$， $L$ $L$$R$$L$$R$，所以 $R$ 不满足 BCNF
    > - 尝试对 $R$ 进行分解，得到 $R_1=(L, K)$， $R_2=(J, L)$，它们都满足 BCNF，但函数依赖关系 $JK\rightarrow L$ 被破坏了
    > 
    > 综上，分解为 BCNF 的过程可能会破坏依赖保持
    > 

## 五、第三范式 Third Normal Forms

!!! note

    1. **数据库的设计目标**
        - 追求无损连接分解、依赖保持、BCNF
        - 任何关系都可以无损连接分解为 BCNF 或 3NF；然而，分解为 BCNF 的过程可能会破坏依赖保持，从而使上述三条目标无法同时满足
    2. **如果不能实现上述目标，可以采取如下的妥协方案**
        - 方案一：使用 BCNF，牺牲依赖保持性
        - 方案二：使用 3NF，它的要求比 BCNF 弱一些，且 3NF  会引入少量冗余，但在分解时一定能保证依赖保持

### 1. 定义

函数依赖集 $F$ 下的关系范式 $R$ 满足 3NF，若对于 $F^+$ 中的每一个函数依赖 $\alpha\rightarrow\beta$，以下三条至少有一条成立：

- $\alpha\rightarrow\beta$ 是平凡的（即 $\beta\subseteq\alpha$）
- $\alpha$ 是 $R$ 的超键（即 $R\subseteq \alpha^+$）
- $(\beta - \alpha)$ 中的每个属性都被 $R$ 的超键所包含

!!! note

    由上述定义，满足 BCNF 的关系范式一定满足 3NF，反之则不一定

!!! example

    > **示例：**
    > 
    > 
    > 考虑 $R=(J, K, L)$， $F=\set{JK\rightarrow L, L\rightarrow K}$
    > 
    > - 考虑 $JK\rightarrow L$， $JK$ 是 $R$ 的超键
    > - 考虑 $L\rightarrow K$， $L$ $L$$R$$L$$R$$K$ 被 $R$ 的超键所包含
    > 
    > 综上， $R$ 不满足 BCNF，但满足 3NF
    > 

### 2. 3NF 引入冗余数据的问题

任何关系都可以无损连接分解为 3NF，但可能引入少量冗余

!!! example

    > **示例：**
    > 
    > 
    > ![image.png](image%2017.png)
    > 
    > - 上图的关系范式满足 3NF
    > - 我们考虑：当一门课暂时没有学生选课时，为了在表中对这门课进行表示，就必须创建一个 $J$ 属性为 NULL 值的元组，从而带来冗余数据问题，使数据库难以维护

### 3. Testing For 3NF

- 为检测关系范式 $R$ 是否满足 3NF，不必如定义所述对 $F^+$ 中每一个 $\alpha\rightarrow\beta$ 进行检验，只需对 $F$ 中的每一个 $\alpha\rightarrow\beta$ 检验即可
- 检测 3NF 是 NP-Hard 问题，然而将关系范式分解为 3NF 可以在多项式时间内完成

### 4. 3NF Decomposition Algorithm

任何关系都可以无损连接分解为 3NF，但可能引入少量冗余

![image.png](image%2018.png)

!!! example

    > **示例：**
    > 
    > 
    > ![image.png](image%2019.png)
    > 

## 六、多值依赖 Multivalued Dependencies（MVDs）

- 考虑这样一个关系范式，它不存在非平凡的函数依赖关系，因此它满足 BCNF，然而其冗余的问题是明显的
- 若对该关系范式进行分解，可以明显改善冗余问题
- 使用 **多值依赖** 的概念对该现象进行描述

![image.png](image%2020.png)

### 1. 定义

多值依赖 $\alpha\rightarrow\rightarrow\beta$ 在关系范式 $R$ 上成立，若对 $r(R)$ 上的任何满足 $t_1[\alpha]=t_2[\alpha]$ 的元组 $t_1$， $t_2$， 都存在元组 $t_3$， $t_4$ 满足下列条件：

- $t_1[\alpha]=t_2[\alpha]=t_3[\alpha]=t_4[\alpha]$
- $t_3[\beta]=t_1[\beta]$
- $t_4[\beta]=t_2[\beta]$
- $t_3[R-\alpha-\beta]=t_2[R-\alpha-\beta]$
- $t_4[R-\alpha-\beta]=t_1[R-\alpha-\beta]$

!!! note

    **多值依赖本质上是对独立性的刻画**

    设有一个关系范式 $R$，其中 $A$、 $B$、 $C$ 是属性集。

    如果对于任意两个元组 $t_1,t_2∈R$，当它们在 $A$ 上的值相同，并且它们在 $B$ 和 $C$ 上的值分别是不同的，那么我们可以找到另外两个元组 $t_3$， $t_4$，它们分别组合了 $A$ 与 $B$ 和 $A$ 与 $C$ 的值，则称：关系 $R$ 中，存在 $A\rightarrow\rightarrow B$ 的多值依赖关系

    简而言之：在已知 $A$ 的值时， $B$ 的所有可能取值与 $C$ 的所有可能取值是 **彼此独立组合** 的


    ![image.png](image%2021.png)

    ![image.png](image%2022.png)

### 2. 性质

1. 函数依赖是多值依赖的特例：若 $\alpha\rightarrow\beta$，则 $\alpha\rightarrow\rightarrow\beta$
2. 若 $\alpha\rightarrow\rightarrow\beta$，则 $\alpha\rightarrow\rightarrow R-\alpha-\beta$
3. 平凡的多值依赖：若 $\beta\subseteq\alpha$，或 $\alpha\cup\beta =R$，则 $\alpha\rightarrow\rightarrow\beta$ 是平凡的（trivial）
4. 闭包：令 $D$ 为函数依赖和多值依赖的一个集合，它的闭包 $D^+$ 就是所有被 $D$ 逻辑蕴含的函数依赖和多值依赖的集合，可通过函数依赖和多值依赖的定义计算
5. 原关系范式进行分解后，子关系范式的多值依赖集 $D_i$ 为：
    
    ![image.png](image%2023.png)
    

## 七、第四范式 Fourth Normal Form

### 1. 定义

函数依赖和多值依赖集 $D$ 下的关系范式 $R$ 满足 4NF，若对于 $D^+$ 中的每一个多值依赖 $\alpha\rightarrow\rightarrow\beta$，以下两条至少有一条成立：

- $\alpha\rightarrow\rightarrow\beta$ 是平凡的（即 $\beta\subseteq\alpha$ 或 $\alpha\cup\beta =R$）
- $\alpha$ 是 $R$ 的超键（即 $R\subseteq \alpha^+$）

!!! note

    由上述定义，满足 4NF 的关系范式一定满足 BCNF，反之则不一定

    严格程度：

    - 4NF > BCNF > 3NF
    - 函数依赖 > 多值依赖

### 2. 4NF Decomposition Algorithm

任何关系都可以无损连接分解为 4NF

![image.png](image%2024.png)

!!! example

    > **示例：**
    > 
    > 
    > ![image.png](image%2025.png)
    >