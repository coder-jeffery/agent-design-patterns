## [第 16 章：资源感知 ]

 

[优化 ]

 

资源感知优化使智能体能够在运行过程中动态监控并

管理计算、时间与财务资源。这有别于简单的规划，后者主要关注动作排序。

资源感知优化要求智能体在指定的资源预算内达成目标，或为优化效率，

就动作执行做出决策。

这包括在更准确但更昂贵的模型与更快、成本更低的模型之间做选择，或决定是否投入额外算力以得到

更精炼的回答，还是返回更快、细节较少的答案。

● **数据用量管理：** 智能体选择检索摘要数据，

而非下载完整数据集，以节省带宽或存储。

● **自适应任务分配：** 在多智能体系统中，智能体根据当前计算负载或可用时间

自行分配任务。

 

[动手代码示例 ]

 

一个用于回答用户问题的智能系统可以评估每个问题的难度。对于简单查询，它使用成本较低的语言模型，例如

Gemini Flash。对于复杂问题，则会考虑使用更强大但更昂贵的语言模型

（如 Gemini Pro）。是否使用更强大的模型还

取决于资源可用性，具体是预算与时间约束。该系统会动态选择合适的模型。

[\# 概念性类 Python 结构，不可运行代码 ]

 

 

[from google.adk.agents import Agent ]

[\# from google.adk.models.lite_llm import LiteLlm \# 若使用 ][ADK 默认 Agent 未直接支持的模型 ]

 

[\# 使用更昂贵的 Gemini Pro 2.5 的智能体 ][gemini_pro_agent = Agent( ]

[name=\"GeminiProAgent\", ]

[model=\"gemini-2.5-pro\", \# 实际模型名称不同时的占位符 ]

[description=\"A highly capable agent for complex queries.\", ]

[instruction=\"You are an expert assistant for complex ][problem-solving.\" ]

[\# 概念性类 Python 结构，不可运行代码 ]

 

 

[from google.adk.agents import Agent, BaseAgent ][from google.adk.events import Event ]

[from google.adk.agents.invocation_context import InvocationContext ][import asyncio ]

 

[class QueryRouterAgent(BaseAgent): ]

[name: str = \"QueryRouter\" ]

[description: str = \"Routes user queries to the appropriate LLM ][agent based on complexity.\" ]

 

[async def \_run_async_impl(self, context: InvocationContext) -\> ][AsyncGenerator\[Event, None\]: ]质量。它还会系统性地评估回答以进行性能监控，

跟踪准确率与相关性等指标，并用于优化。

 

此外，其反馈可触发强化学习或微调；例如，若持续

识别出 Flash 模型回答不足，则可据此完善路由

智能体的逻辑。批评者智能体虽不直接管理预算，但通过识别次优路由选择——例如将简单查询导向 Pro 模型，或将复杂查询导向 Flash 模型，从而

导致结果不佳——间接贡献于预算管理。这为改进资源分配与

节省成本提供了依据。

 

批评者智能体可配置为仅审阅回答智能体生成的文本，或同时审阅原始查询与生成文本，从而对

回答与初始问题的契合度进行全面评估。提示词还应鼓励同时识别优点与不足，

并必须指导智能体如何组织与呈现其反馈。

 

[动手代码（OpenAI） ]

 

该系统采用资源感知优化策略，以高效处理用户查询。

它先将每个查询分为三类，以确定

最合适且最具成本效益的处理路径。这种方法避免了

在简单请求上浪费计算资源，同时确保复杂查询获得应有的关注。三类为：

 

● simple：适用于可直接回答、无需

复杂推理或外部数据的简单问题。

[\"请在 .env 文件中设置 OPENAI_API_KEY、GOOGLE_CUSTOM_SEARCH_API_KEY 和 ][GOOGLE_CSE_ID。\" ]

[) ]

 

[client = OpenAI(api_key=OPENAI_API_KEY) ]

 

[\# \-\-- 步骤 1：对提示词分类 \-\-- ]

[def classify_prompt(prompt: str) -\> dict: ]

[system_message = { ]

[\"role\": \"system\", ]

[\"content\": ( ]

[\"You are a classifier that analyzes user prompts and ][returns one of three categories ONLY:\\n\\n\" ]

[\"- simple\\n\" ]

[\"- reasoning\\n\" ]

[\"- internet_search\\n\\n\" ]

[try: ]

[response = requests.get(url, params=params) ]

[response.raise_for_status() ]

[results = response.json() ]

 

[if \"items\" in results and results\[\"items\"\]: ]

[return \[ ]

[{ ]

[\"title\": item.get(\"title\"), ]

[\"snippet\": item.get(\"snippet\"), ]

[\"link\": item.get(\"link\"), ]

[} ]

[for item in results\[\"items\"\] ]

[\] ]

[Query: {prompt}\"\"\" ]

 

 

[response = client.chat.completions.create( ]

[model=model, ]

[messages=\[{\"role\": \"user\", \"content\": full_prompt}\], ]

[temperature=1, ]

[) ]

 

[return response.choices\[0\].message.content, model ]

 

[\# \-\-- 步骤 4：组合路由器 \-\-- ]

[def handle_prompt(prompt: str) -\> dict: ]

[classification_result = classify_prompt(prompt) ]

 

[\# print(\"\\n] [🔍] [\# 删除或注释掉下一行，以避免重复打印 ][ Classification Result:\", classification_result) ]随后生成最终回答，并根据

分类选择合适的 OpenAI 模型。对于互联网搜索类查询，搜索结果会作为上下文提供给模型。主函数 handle_prompt 编排该工作流，

在生成回答前调用分类函数，并在需要时调用搜索函数。

它返回分类结果、所用模型以及生成的答案。该

系统将不同类型的查询高效导向优化方法，以获得更好的回答。

 

[动手代码示例（OpenRouter） ]

 
