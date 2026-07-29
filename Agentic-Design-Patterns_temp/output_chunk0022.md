["message": f"User login tracked. Total logins: ]

[{login_count}." ]

[} ]

 

[\# \-\-- Demonstration of Usage \-\-- ]

[\# In a real application, an LLM Agent would decide to call this ][tool. ]

[\# Here, we simulate a direct call for demonstration purposes. ]

 

[\# 1. Setup ]

[session_service = InMemorySessionService() ][app_name, user_id, session_id = "state_app_tool", "user3", ]["session3" ]

[\# and more robust. ]

 

这段代码演示了在应用中用基于工具的方法管理用户会话状态。它定义了函数 *log_user_login*，该函数充当一个工具。当用户登录时，该工具负责更新会话状态。

该函数接收由 Google ADK 提供的 ToolContext 对象，用于访问和修改

会话的状态字典。在工具内部，它会递增 *user:login_count*，将

t*ask_status* 设为 "active"，记录 *user:last_login_ts（时间戳）*，并添加临时标志 temp:validation_needed。

 

代码的演示部分模拟了如何使用该工具。它设置了

内存会话服务，并用一些预定义状态创建初始会话。随后手动创建 ToolContext，以模拟智能体在多次交互中保留信息或访问外部数据时的环境，

因此需要长期知识管理。这由 MemoryService 提供支持。

 

[\# Example: Using InMemoryMemoryService ]

[\# This is suitable for local development and testing where data ][\# persistence across application restarts is not required. ][\# Memory content is lost when the app stops. ][from google.adk.memory import InMemoryMemoryService ][memory_service = InMemoryMemoryService() ]

 

会话与状态可理解为单次聊天会话的短期记忆，

而由 MemoryService 管理的长期知识

则充当持久且可搜索的知识库。该知识库可能包含

[\# Optional configuration for retrieval behavior ][SIMILARITY_TOP_K = 5 \# Number of top results to retrieve ][VECTOR_DISTANCE_THRESHOLD = 0.7 \# Threshold for vector similarity ]

 

 

[memory_service = VertexAiRagMemoryService( ]

[rag_corpus=RAG_CORPUS_RESOURCE_NAME, ]

[similarity_top_k=SIMILARITY_TOP_K, ]

[vector_distance_threshold=VECTOR_DISTANCE_THRESHOLD ][) ]

[\# When using this service, methods like add_session_to_memory ][\# and search_memory will interact with the specified Vertex AI ][\# RAG Corpus. ]

 

[实操代码：LangChain 中的记忆管理 ]

**ChatMessageHistory：手动记忆管理。** 若要在正式链之外对对话历史进行直接、简单的控制，ChatMessageHistory 类

 

非常合适。它支持手动跟踪对话往来。

 

[from langchain.memory import ChatMessageHistory ]

 

[\# Initialize the history object ]

[history = ChatMessageHistory() ]

 

[\# Add user and AI messages ]

[history.add_user_message("I'm heading to New York next week.") ][history.add_ai_message("Great! It's a fantastic city.") ]

 

[\# Access the list of messages ]将此记忆接入 LLMChain，可使模型访问

对话历史并给出符合上下文的回复

 

[from langchain_openai import OpenAI ]

[from langchain.chains import LLMChain ]

[from langchain.prompts import PromptTemplate ][from langchain.memory import ConversationBufferMemory ]

 

[\# 1. Define LLM and Prompt ]

[llm = OpenAI(temperature=0) ]

[template = """You are a helpful travel agent. ]

 

[Previous conversation: ]

[{history} ]

[SystemMessagePromptTemplate, ]

[HumanMessagePromptTemplate, ]

[) ]

 

[\# 1. Define Chat Model and Prompt ]

[llm = ChatOpenAI() ]

[prompt = ChatPromptTemplate( ]

[messages=\[ ]

[SystemMessagePromptTemplate.from_template("You are a friendly ][assistant."), ]

[MessagesPlaceholder(variable_name="chat_history"), ]

[HumanMessagePromptTemplate.from_template("{question}") ]

[\] ]

[) ]

 

[\# 2. Configure Memory ]

少样本示例提示，即智能体从过去成功的

交互序列中学习，从而正确执行任务。

● **程序性记忆：记住规则：** 这是关于如何

执行任务的记忆——智能体的核心指令与行为，通常包含在

其系统提示词中。智能体修改自身提示词以

适应和改进的做法很常见。一种有效的技术是“反思”，即向智能体提供当前指令与近期交互，然后要求它

完善自身指令。

 

下面是伪代码，演示智能体如何用反思来更新存储在 LangGraph BaseStore 中的程序性记忆

 

[\# Node that updates the agent's instructions ]

LangGraph 将长期记忆以 JSON 文档形式存入存储。每条记忆按自定义命名空间（类似文件夹）和独立键（类似

 

文件名）组织。这种层次结构便于组织与检索

信息。以下代码演示如何使用 InMemoryStore 进行 put、get

与 search 记忆操作。

 

[from langgraph.store.memory import InMemoryStore ]

 

[\# A placeholder for a real embedding function ][def embed(texts: list\[str\]) -\> list\[list\[float\]\]: ]

[\# In a real application, use a proper embedding model ]

[namespace, ]

[filter={"my-key": "my-value"}, ]

[query="language preferences" ]

[) ]

[print("Search Results:", items) ]

 

[Vertex Memory Bank ]

 

Memory Bank 是 Vertex AI Agent Engine 中的托管服务，可为智能体提供持久的长期记忆。该服务使用 Gemini 模型异步

分析对话历史，以提取关键事实与用户偏好。

 

这些信息按用户 ID 等已定义范围持久存储并组织，

Memory Bank 与 Google ADK 无缝集成，可提供

 

开箱即用的体验。对于使用其他智能体框架（如 LangGraph 与 CrewAI）的用户，Memory Bank 也通过直接 API 调用提供支持。

展示这些集成的在线代码示例已可供

感兴趣的读者查阅。

 

[一览]
