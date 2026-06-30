# Chapter 11: Requirements Modeling: Behaviour, Patterns, and Web/Mobile Apps

## 11.1 行为建模 Behavioral Modeling

1. **定义：**行为模型用于描述软件系统如何对外部事件或刺激作出响应。它关注系统在运行过程中的动态行为。
2. **构建行为模型的步骤**
    - **分析所有用例（Use Case）：**充分理解系统内部的交互流程。
    - **识别事件（Event）：**找出触发系统交互的外部事件，理解事件与系统对象之间的关系。
    - **为每个用例创建顺序图（Sequence Diagram）：**描述对象之间的消息传递顺序。
    - **构建状态图（State Diagram）：**描述系统状态以及状态转换。
    - **检查行为模型：**验证模型的准确性与一致性。
3. **状态的两种视角**
    
    在行为建模中，需要考虑两类状态：
    
    - **类的状态（Class State）：**系统运行过程中每个对象或类的状态变化。
    - **系统状态（System State）：**从系统外部观察到的整体状态变化。
4. **状态图（State Diagram）**
    
    状态图用于描述：
    
    - 系统的不同状态
    - 状态之间的转换
    - 触发状态转换的事件
    
    ![image.png](Chapter%2011%20Requirements%20Modeling%20Behaviour,%20Patter/image.png)
    
5. **顺序图（Sequence Diagram）**
    
    顺序图重点描述：“谁在什么时候向谁发送什么消息”。
    
    ![image.png](Chapter%2011%20Requirements%20Modeling%20Behaviour,%20Patter/image%201.png)
    

## 11.2 面向流程的建模 Flow-Oriented Modeling

1. 基本思想：系统可以抽象为：**数据 + 功能**
    
    ![image.png](Chapter%2011%20Requirements%20Modeling%20Behaviour,%20Patter/image%202.png)
    
2. **数据流图（Data Flow Diagram，DFD）**
    
    数据流图用于描述：数据在系统中的流动与处理过程。
    
    数据流图的基本元素：
    
    - **外部实体（External Entity）**
        - 系统外部的参与者，例如：用户
    - **处理过程（Process）**
        - 对数据进行加工处理
    - **数据存储（Data Store）**
        - 存储数据的地方，例如：数据库、文件
    - **数据流（Data Flow）**
        - 表示数据在系统中的流动
    
    ![image.png](Chapter%2011%20Requirements%20Modeling%20Behaviour,%20Patter/image%203.png)
    
    ![image.png](Chapter%2011%20Requirements%20Modeling%20Behaviour,%20Patter/image%204.png)
    
3. **与数据流层次结构（Data Flow Hierarchy）**
    - 复杂过程可以继续拆分，称为**数据流细化（Refinement）**。例如：Get a book 可以分解为 Find book position + Get a book。
    - 经过细化的数据流，通常采用**分层结构**。这种方法称为**逐层细化（Top-down Refinement）**。
        - Level 0（上下文图）：系统被看作一个整体 P
        - Level 1：将系统拆分为多个子过程 P1 - P5
        - Level 2：继续细化某个子过程……
    
    ![image.png](Chapter%2011%20Requirements%20Modeling%20Behaviour,%20Patter/image%205.png)
    

## 11.3 Web应用需求建模 Requirements Modeling for WebApps

1. **在以下情况下，需要进行需求分析：**
    - Web或移动应用规模较大或复杂
    - 利益相关者（Stakeholders）数量多
    - 开发人员数量多
    - 团队成员彼此不熟悉
    - 项目的成功对业务影响重大（have a strong bearing）
2. **Web应用需求分析的五个方面**
    - 内容分析（Content Analysis）：描述Web应用中的文本、图像、视频、音频。
    - 交互分析（Interaction Analysis）：通过用例描述用户如何与系统交互。
    - 功能分析（Functional Analysis）：确定系统功能，包括 Web 应用对内容执行的操作，以及相关处理逻辑。
    - 配置分析（Configuration Analysis）：关注系统运行环境。
    - 导航分析（Navigation Analysis）：研究用户如何在系统中导航。
3. **配置分析细则**
    - 服务器端需要定义：
        - 服务器硬件、操作系统
        - 互操作性（Interoperability）
        - 接口与通信协议（Appropriate interfaces，communication protocols ）
    - 客户端需要定义：浏览器配置、测试需求。
4. **导航分析细则**
    - 重点问题包括：
        - 哪些页面需要更容易访问（需要更少的导航步骤）？
        - 是否需要为某些内容附加优先级？
        - 如何处理导航错误？
        - 是否优先提供相关内容的导航？
        - 是否使用搜索功能？
        - 是否根据用户行为提供推荐导航？
        - 是否记录用户导航日志？
    - 导航设计需要思考的问题
        - 用户交互的每个环节都应该提供完整的导航地图或菜单（而不是单一的“返回”链接或有向指针）吗？
        - 导航设计应以最常见的用户行为为驱动，还是基于定义WebApp元素的重要性？
        - 用户能否“存储”他之前通过WebApp的导航，以加快未来的使用速度？
        - 最优导航应针对哪个用户类别设计？
        - WebApp以外的链接应该如何处理？是叠加现有的浏览器窗口吗？作为新的浏览器窗口？作为一个独立的框架？