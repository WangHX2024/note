# Chapter 7: Principles that Guide Practice

1. **指导过程的原则**（Principles that Guide Process）
    - 保持敏捷（Be agile）： 无论选择何种过程模型（Process Model），敏捷开发的基本原则都应指导你的方法。
    - 在每一步都关注质量（Focus on quality at every step）： 每个过程活动的退出条件（Exit condition）都应关注工作产品（Work product）的质量。
    - 准备好进行调整（Be ready to adapt）： 过程不是教条，应根据问题、人员和项目约束（Constraints）调整方法。
    - 建立一支高效的团队（Build an effective team）： 软件工程的底线是人，应建立具有相互信任和尊重的自组织团队（Self-organizing team）。
    - 建立沟通和协调机制（Establish mechanisms for communication and coordination）： 防止重要信息遗漏，确保利益相关者（Stakeholders）协同工作。
    - 管理变更（Manage change）： 建立机制来管理请求、评估、批准和实施变更（Change）的方式。
    - 评估风险（Assess risk）： 软件开发中很多事情都可能出错，必须建立应急计划（Contingency plans）。
    - 创建能为他人提供价值的工作产品（Create work products that provide value for others）： 只创建那些能为后续活动提供价值产出的工作产品。
2. **指导实践的原则**（Principles that Guide Practice）
    - 分而治之（Divide and conquer）： 强调关注点分离（Separation of Concerns, SoC）。
    - 理解抽象的使用（Understand the use of abstraction）： 抽象（Abstraction）是对复杂元素的简化，用于在单一短语中传达含义。
    - 争取一致性（Strive for consistency）： 熟悉的上下文（Context）使软件更易于使用。
    - 关注信息的传递（Focus on the transfer of information）： 特别注意接口（Interfaces）的分析、设计、构建和测试。
    - 构建表现出有效模块化的软件（Build software that exhibits effective modularity）： 模块化（Modularity）是实现关注点分离的机制。
    - 寻找模式（Look for patterns）： 寻找重复出现的问题的解决方案（Patterns）。
    - 多视角表示（Represent from different perspectives）： 尽可能从多个不同的视角来表示问题及其解决方案。
    - 考虑维护（Remember that someone will maintain the software）： 记住总会有人来维护软件。
3. **沟通原则**（Communication Principles）
    - 倾听（Listen）： 专注于说话者的言语。
    - 沟通前做好准备（Prepare before you communicate）： 在会面前理解问题。
    - 应当有人主持该活动（Someone should facilitate the activity）： 由主持人（Facilitator）保持对话方向并调解冲突。
    - 面对面沟通是最好的（Face-to-face communication is best）： 结合相关信息的其他表示形式效果更好。
    - 记笔记并记录决策（Take notes and document decisions）： 记录员（Recorder）记录要点。
    - 争取协作（Strive for collaboration）： 结合团队成员的集体知识以达成共识（Consensus）。
    - 保持专注，模块化你的讨论（Stay focused, modularize your discussion）： 避免话题跳跃。
    - 如果某些事情不清楚，画个图（If something is unclear, draw a picture）。
    - 及时推进（Move on）： 达成一致、无法一致或功能不明时，先继续进行。
    - 谈判不是一场比赛（Negotiation is not a contest）： 双赢（Win-win）效果最好。
4. **计划原则**（Planning Principles）
    - 理解项目的范围（Understand the scope of the project）： 范围（Scope）为团队提供目的地。
    - 让客户参与计划活动（Involve the customer in the planning activity）： 客户定义优先级（Priorities）和约束。
    - 认识到计划是迭代的（Recognize that planning is iterative）： 计划并非一成不变，会随情况变化。
    - 基于已知情况进行估算（Estimate based on what you know）： 提供工作量（Effort）、成本和持续时间的指示。
    - 考虑风险（Consider risk）： 识别高影响、高概率的风险并制定应急计划。
    - 要现实（Be realistic）： 考虑人员并非 100% 时间都在工作。
    - 调整粒度（Adjust granularity）： 根据需要调整计划的详细程度。
    - 定义如何确保质量（Define how you intend to ensure quality）： 明确质量保证（Quality assurance）方法。
    - 描述如何适应变更（Describe how you intend to accommodate change）： 即使是最好的计划也可能被变更废止。
    - 频繁跟踪计划（Track the plan frequently）： 及时调整以防进度落后。
5. **建模原则**（Modeling Principles）
    - 需求模型（Requirements Models）： 也称分析模型（Analysis Models），描述信息域、功能域和行为域（Information, functional, and behavioral domains）。
    - 设计模型（Design Models）： 表示架构、用户界面和组件级细节（Architecture, user interface, and component-level detail）。
    - 敏捷建模原则（Agile Modeling Principles）：主要目标是构建软件而非模型。
        - 轻装上阵（Travel light），不创建多余模型。
        - 追求最简单的模型（Simplest model）。
        - 适应变更、明确目的、注重实用性、快速反馈（Feedback）。
6. **需求建模原则**（Requirements Modeling Principles）
    - 表示信息域。
    - 定义软件执行的功能（Functions）。
    - 表示软件的行为（Behavior）。
    - 采用分层（Layered/Hierarchical）方式揭示细节。
    - 从基本信息转向实现细节（Implementation detail）。
7. **设计建模原则**（Design Modeling Principles）
    - 可追溯性（Traceable）： 设计应可追溯到需求模型。
    - 考虑架构（Architecture）： 始终关注系统的架构。
    - 数据设计（Design of data）： 与处理功能的设计同样重要。
    - 精心设计接口（Interfaces）： 关注内部和外部接口。
    - 用户界面设计（User interface design）： 根据端用户（End-user）需求调整，强调易用性。
    - 功能独立（Functionally independent）： 组件级设计应保持独立性。
    - 松散耦合（Loosely coupled）： 组件之间以及与环境之间应保持松散耦合。
8. **构建原则**（Construction Principles）
    - 准备原则（Preparation Principles）： 在编码前理解问题、理解设计原则、选择语言、选择编程环境、创建单元测试（Unit tests）。
    - 编码原则（Coding Principles）： 遵循结构化编程（Structured programming）、考虑结对编程（Pair programming）、选择合适的数据结构、编写自文档化代码（Self-documenting code）。
    - 验证原则（Validation Principles）： 进行代码走查（Code walkthrough）、执行单元测试、进行代码重构（Refactor）。
9. **测试原则**（Testing Principles）
    - 所有测试应可追溯到客户需求。
    - 提前计划测试。
    - 帕累托法则（Pareto principle）适用于测试（即 80% 的错误通常隐藏在 20% 的代码中）。
    - 从“小规模”测试（In the small）向“大规模”测试（In the large）推进。
    - 穷尽测试（Exhaustive testing）是不可能的。
    - 测试静态分析（Static testing）可以产生很高的结果。
10. **部署原则**（Deployment Principles）
    - 管理客户期望（Customer expectations）。
    - 组装并测试完整的交付包（Delivery package）。
    - 建立支持制度（Support regime）。
    - 提供教学材料（Instructional materials）。
    - 修复缺陷（Buggy software）后再交付。