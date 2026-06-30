# 期末复习背诵

# Testing Strategy

1. 测试策略（10 条）
    - 单元测试：验证每个函数或者方法是否正确
    - 内容测试：验证软件中的文本数据是否完整一致
    - 接口测试：验证不同模块之间是否能够正常通信，API测试和UI界面测试
    - 导航测试：验证前端交互导航是否正确
    - 集成测试：验证多个模块之间集成是否正确
    - 回归测试：验证更新后旧代码是否还有问题。
    - 配置测试：验证配置，如不同硬件和网络环境下是否正常。
    - 性能测试：验证不同负载下的性能表现，响应时间，吞吐量，资源占用
    - 安全测试：保证软件能够抵御攻击，保证信息安全。
    - 认证测试：保证软件符合法规。

# CH2 通用过程模型

1. 框架活动（5 个）
    - Communication (与客户合作，获取需求)
    - Planning (构建⽬标，描述难点、需求，定义⼯作计划)
    - Modeling (构建模型⽅便理解软件需求和设计)
    - Construction (软件开发和测试)
    - Deployment (软件交付和⽤户评估反馈)

# CH5 敏捷开发

1. Why Agile
    - Effective Response to change/communication
    - Driven by customer's requirement
    - Self-organization
    - Rapid incremental delivery
    - 优点：开发周期短，随时应对需求变化
    - 缺点：需要团队的高效协作、沟通，不适用于人数规模大的开发团队，需要与客户频繁沟通协作

# CH7 软件开发原则

1. 沟通原则
    - 倾听
    - 沟通前准备
    - 每次沟通会议都应有⼈引导
    - 面对面沟通
    - 记笔记，将决策形成⽂档
    - 坚持协作
    - 保持专注，讨论模块化
    - 对不清楚的东⻄画个图
    - 无论同意与否、或此时无法阐明，先继续
    - 谈判不是游戏，双赢才是正义

# CH8 需求工程

1. 利益相关者：直接或间接影响软件系统开发、交付、运营，或受其影响的个人、团队或组织
    - Senior managers who define the business issues that often have significant influence on the project .
    - Project (technical) managers who must plan, motivate, organize, and control the practitioners who do software work.
    - Practitioners who deliver the technical skills that are necessary to engineer a product or application.
    - Customers who specify the requirements for the software to be engineered and other stakeholders who have a peripheral interest in the outcome.
    - End-users who interact with the software once it is released for production use.
2. 需求工程的任务（8 个）
    - Inception（起始）: 对项⽬建⽴基本的理解(Context-Free Questions)，识别利益相关者
    - Elicitation（获取）: 询问客户的需求(QFD: Normal / Expected / Exciting Requirements，Non-Functional Requirements，Use Cases)
    - Elaboration（细化）: 建⽴需求模型
    - Negotiation（协商）: 参与各⽅均能达到⼀定的满意度，实现双赢。
    - Monitoring（跟踪）
    - Specification（规格说明）:  ⼀个规格说明可以是⼀份写好的⽂档、⼀套图形化的模型、⼀个形式化的数学模型、⼀组使⽤场景、⼀个原型或上述各项的任意组合。
    - Validation（验证）: 验证阶段不做技术评审。验证的维度：Consistency / Omissions / Ambiguity
    - Management: 需求管理是⽤于帮助项⽬组在项⽬进展中标识、控制和跟踪需求以及需求变更的⼀组活动。
3. QFD
    - Normal requirements are written in the project requirements to meet the requirements of Party A’s software requirements
    - Expected requirements are not written in the project requirements, but as a mature software engineering should achieve software requirements
    - Exciting requirements are requirements that are not written into the project requirements, that are not anticipated, that do not affect the functionality of the program, but that can greatly enhance the user experience by having them
4. 四种需求分析模型
    
    ![image.png](%E6%9C%9F%E6%9C%AB%E5%A4%8D%E4%B9%A0%E8%83%8C%E8%AF%B5/image.png)
    
5. 构建分析模型的经验法则 Rules of Thumb Emphasis
    - 模型应聚焦于问题或业务领域内可见的需求。
    - 抽象层次应相对较高。
    - 分析模型的每个元素都应有助于整体理解软件需求，并为系统的信息领域、功能和行为提供洞察。
    - 在需求分析阶段，推迟考虑现实问题（基础设施和其他非功能性模型），应在设计阶段再考虑。
    - 最小化系统耦合。
    - 确保分析模型对所有利益相关者都有价值。
    - 保持模型尽可能简单。

# CH13 架构设计

1. 架构类别/风格的类别
    - Data-Centered
    - Data Flow
    - Call and Return
    - Layered
2. 架构模式（Architectural Patterns）
    - 并发性（Concurrency）
    - 持久化（Persistence）
    - 分布性（Distribution）
3. 判断架构好不好的依据
    - 经济性（Economy）：最佳软件应精简，依靠抽象减少不必要的细节 。
    - 可见性（Visibility）：架构决策及其原因应对后续维护的工程师显而易见 。
    - 间距（Spacing）：实现关注点分离，且不引入隐藏的依赖关系 。
    - 对称性（Symmetry）：确保系统属性的一致性与平衡 。
    - 涌现性（Emergence）：关注自组织的行为与控制 。

# CH14 组件设计

1. 组件的基本设计原则（7 条）
    - 开闭原则（OCP）：构件允许扩展，而不允许修改。
    - 里氏替换原则（LSP）：子类应当可以替换其基类。
    - 依赖倒置原则（DIP）：依赖于抽象，而非具体实现。
    - 接口隔离原则（ISP）：多个针对特定客户的接口优于一个通用的单一接口。
    - 发布重用等价原则（REP）：重用的粒度（granule）就是发布的粒度。
    - 共同封闭原则（CCP）：一起修改的类应当封装在一起。
    - 共同重用原则（CRP）：不在一起重用的类不应组合在一起。

# CH15 用户界面设计

1. 用户界面设计的黄金法则
    - 法则一：让用户拥有控制权
    - 法则二：减轻用户的记忆负担
    - 法则三：保持界面一致性
2. WebApp 审美设计（Aesthetic design）的要求
    - 不要害怕留白。
    - 强调内容。
    - 按从左上到右下组织布局元素。
    - 在页面内按地理区域对导航、内容和功能进行分组。
    - 不要使用滚动条来扩展你的地盘。
    - 设计布局时考虑分辨率和浏览器窗口大小。

# CH22 软件测试

1. 什么是好的软件测试
    - Has a high probability of finding an error
    - Not redundant
    - Should be capable of uncovering a whole class of errors
    - Should not be too simple or too complete

# CH32 产品度量

1. 比较适合历史数据明确的估算是 LOC。 FP 是功能点估算，从用户角度、输入输出之类的功能方面的，适合 FP。
2. 选择 FP 的理由
    - 理由一：编程语言无关（Programming language independent）
    - 理由二：在软件过程早期就可以使用（Countable early in the process）
        
        LOC 要等代码写出来才能数；FP 只需要需求文档就可以估算，可在项目启动阶段就用于早期成本估算。
        
    - 理由三：不"惩罚"精炼简洁的实现（Doesn't penalize inventive implementations）
        
        同样的功能，高手用 50 行 Python 实现，新手用 200 行实现。LOC 会"奖励"冗余代码，FP 只认功能，不认行数。
        
    - 理由四：更易度量复用组件的影响（Easier to measure impact of reuse）
        
        当一个组件被复用时，新增功能不需要重新开发，LOC 增量为零，但用户侧的功能确实增加了。FP 能更准确地捕捉这种场景的生产力贡献。
        

# CH35 风险管理

1. RMMM
    - Risk Mitigation 风险缓解: How can we avoid the risks
    - Risk Monitering 风险监控: What factor to track to determine whether the risk is becoming real
    - Risk Management 风险管理: What contingency plan do we have
2. RMMM 计划：
    1. 项目： EMSS 系统
    2. 风险类型： 人力资源风险 或 红外硬件风险
    3. 优先级（1 低 ... 5 严重）： 3
    4. 风险因素： 在软件开发过程中，出现人员变动，例如软件工程师离职。
    5. 可能性： 40%
    6. 影响： 软件开发流程延迟
    7. 监控方法：
        1. 监控工程师的情绪；
        2. 检查工程师的生产力；
        3. 调查竞争对手的薪资水平
    8. 缓解措施（应急方案）：
        1. 组织团队建设活动；
        2. 丰富文档；
        3. 频繁的技术会议或培训；
        4. 建立人力资源储备库。
    9. 管理（资源预估）：
        1. 寻找新人；
        2. 工作交接；
        3. 总结原因

# CH36 维护与再工程

1. Reengineering paradiag 的六大活动
    
    ![image.png](%E6%9C%9F%E6%9C%AB%E5%A4%8D%E4%B9%A0%E8%83%8C%E8%AF%B5/image%201.png)