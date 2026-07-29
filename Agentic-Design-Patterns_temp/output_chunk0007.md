## [第 2 章：路由 ]

 

[路由模式概览 ]

 

虽然通过提示链进行顺序处理是用大语言模型执行确定性、线性工作流的基础技术，

但其适用性在需要自适应响应的场景中受到限制。现实世界的智能体式系统往往必须根据偶然因素，

在多种可能的行动之间进行仲裁，例如环境状态、用户输入，或前序操作的结果。

这种动态决策能力——将控制流导向不同的专用函数、工具或子流程——

是通过一种称为路由的机制实现的。

 

路由将条件逻辑引入智能体的运行框架，使其能够

用户查询并仅输出类别：'Order Status'、'Product Info'、'Technical

Support' 或 'Other'。" 智能体式系统随后读取该输出，并据此引导工作流。

[● ]**基于嵌入的路由：** 可将输入查询转换为向量

嵌入（参见检索增强生成，第 14 章）。随后将该嵌入与

代表不同路由或能力的嵌入进行比较。查询被路由到嵌入最相似的那条路由。这对语义路由很有用，

其决策基于输入的含义，而非仅仅基于

关键词。

[● ]**基于规则的路由：** 这涉及使用预定义的规则或逻辑（例如 if-else

语句、switch 分支），依据从输入中提取的关键词、模式或结构化数据。

这通常比基于大语言模型的路由更快、更确定，

但在处理细微或新颖输入时灵活性较差。

● **基于机器学习模型的路由**：它采用判别式模型，由函数或基于模型的评估来决定计算图中

各节点之间的转换。

 

路由的实现使系统能够超越确定性的

顺序处理。它有助于开发更具适应性的执行流，

能够对更广泛的输入与状态变化做出动态且恰当的响应。

 

[实际应用与用例 ]

 

路由模式是设计自适应智能体式系统时的关键控制机制，

使其能够根据可变输入与内部状态动态改变执行路径。

其效用跨越多个领域，提供必要的条件逻辑层。在变化条件下就完成任务的最有效方法做出决策。

 

[动手代码示例（LangChain） ]

 

在代码中实现路由，需要定义可能的路径以及决定走哪条路径的逻辑。

像 LangChain 和 LangGraph 这样的框架为此提供了

特定的组件与结构。LangGraph 基于状态的图结构对于可视化和实现路由逻辑尤其直观。

 

这段代码演示了一个使用 LangChain 与 Google

生成式 AI 的简易类智能体系统。它设置了一个「协调器」，根据请求意图（预订、信息查询或不明确）

将用户请求路由到不同的模拟「子智能体」处理器。系统使用大语言模型对请求进行分类，然后 [temperature=0) ]

[print(f\"Language model initialized: {llm.model}\") ][except Exception as e: ]

[print(f\"Error initializing language model: {e}\") ]

[llm = None ]

 

[\# \-\-- 定义模拟的子智能体处理器（等价于 Google ADK ][sub_agents) \-\-- ]

 

[def booking_handler(request: str) -\> str: ]

[\"\"\"模拟预订智能体处理请求。\"\"\" ]

[print(\"\\n\-\-- DELEGATING TO BOOKING HANDLER \-\--\") ]

[return f\"Booking Handler processed request: \'{request}\'. Result: ][Simulated booking action.\" ]

 

[def info_handler(request: str) -\> str: ][based on sub_agents) \-\-- ]

[\# 使用 RunnableBranch 根据 router 链的输出进行路由。 ]

 

[\# 定义 RunnableBranch 的各分支 ][branches = { ]

[\"booker\": RunnablePassthrough.assign(output=lambda x: ][booking_handler(x\[\'request\'\]\[\'request\'\])), ]

[\"info\": RunnablePassthrough.assign(output=lambda x: ][info_handler(x\[\'request\'\]\[\'request\'\])), ]

[\"unclear\": RunnablePassthrough.assign(output=lambda x: ][unclear_handler(x\[\'request\'\]\[\'request\'\])), ][} ]

 

[\# 创建 RunnableBranch。它接收 router 链的输出 ][\# 并将原始输入（'request'）路由到相应的 ][handler. ]

[print(\"\\n\-\-- Running with an info request \-\--\") ]

[request_b = \"What is the capital of Italy?\" ]

[result_b = coordinator_agent.invoke({\"request\": request_b}) ]

[print(f\"Final Result B: {result_b}\") ]

 

[print(\"\\n\-\-- Running with an unclear request \-\--\") ]

[request_c = \"Tell me about quantum physics.\" ]

[result_c = coordinator_agent.invoke({\"request\": request_c}) ]

[print(f\"Final Result C: {result_c}\") ]

 

[if \_\_name\_\_ == \"\_\_main\_\_\": ]

[main() ]

 

如前所述，这段 Python 代码使用路由构建了一个简易的类智能体系统；在 Google ADK 范式中，路由通常通过定义一组离散的

「工具」来实现，这些工具代表智能体的各项功能。响应用户查询时选择合适工具，由框架的内部逻辑管理，

该逻辑借助底层模型将用户意图匹配到正确的功能处理器。

 

这段 Python 代码演示了一个 Google ADK

应用示例，使用 Google ADK 库。它设置了一个「Coordinator」智能体，根据已定义的指令将用户请求路由到专用子智能体（「Booker」负责预订，「Info」负责一般

信息）。子智能体随后使用特定工具来

模拟处理请求，展示了智能体系统中的基本委派模式。

 

[\# Copyright (c) 2025 Marco Fago ]

[\# ]

[request: 用户的问题。 ]

[Returns: ]

[一条表明信息请求已处理的消息。 ]

[\"\"\" ]
