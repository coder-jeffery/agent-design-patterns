智能体将其分解为独立的子查询。它会发起不同的 **简言之：** 智能体式检索增强生成代表了标准

检索模式的一次精妙演进，将其从被动的数据流水线转变为主动的

问题解决框架。通过嵌入能够评估

来源、调和冲突、分解复杂问题并使用外部工具的推理层，智能体显著提升了所生成答案的可靠性与深度。这一

进展使 AI 更加可信且更有能力，尽管它也带来了

系统复杂度、延迟与成本方面的重要权衡，必须谨慎

管理。

 

[实际应用与用例 ]

 

知识检索（检索增强生成）正在改变大语言模型

在各行业中的使用方式，增强其提供更准确信息的能力 [实操代码示例（ADK） ]

 

为说明知识检索（检索增强生成）模式，我们来看三个示例。

 

首先，是如何使用 Google 搜索进行检索增强生成，并将大语言模型锚定到搜索结果。

由于检索增强生成涉及访问外部信息，Google 搜索工具是内置

检索机制的直接示例，可用于增强大语言模型的知识。

 

[from google.adk.tools import google_search ][from google.adk.agents import Agent ]

 

[search_agent = Agent( ]

[name="research_assistant", ]

[model="gemini-2.0-flash-exp", ]

[instruction="You help users research topics. When asked, use the ][to retrieve. ]

[# 这控制检索增强生成服务将返回多少相关文档块。 ]

[SIMILARITY_TOP_K = 5 ]

 

[# 为向量距离阈值定义一个可选参数。 ][# 该阈值决定检索结果允许的最大语义距离； ]

[# 距离大于该值的结果可能会被过滤掉。 ]

[VECTOR_DISTANCE_THRESHOLD = 0.7 ]

 

[# 初始化 VertexAiRagMemoryService 实例。 ][# 这将建立与你的 Vertex AI RAG Corpus 的连接。 ][# - rag_corpus: 指定你的 RAG Corpus 的唯一标识符。 ][# - similarity_top_k: 设置要返回的相似结果的最大数量 ][import dotenv ]

 

[# 加载环境变量（例如 OPENAI_API_KEY） ][dotenv.load_dotenv() ]

[# 设置你的 OpenAI API 密钥（确保已从 .env 加载或在此设置） ][# os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY" ]

 

[# --- 1. 数据准备（预处理） --- ][# 加载数据 ]

[url = ]

["https://github.com/langchain-ai/langchain/blob/master/docs/docs/how_ ] [to/state_of_the_union.txt" ]

[res = requests.get(url) ]

 

[with open("state_of_the_union.txt", "w") as f: ]

[f.write(res.text) ]

[documents: List[Document] ]

[generation: str ]

 

[# --- 3. 定义节点（函数） --- ]

 

[def retrieve_documents_node(state: RAGGraphState) -> RAGGraphState: ]

["""根据用户问题检索文档。""" ]

[question = state["question"] ]

[documents = retriever.invoke(question) ]

[return {"documents": documents, "question": question, ]["generation": ""} ]

 

[def generate_response_node(state: RAGGraphState) -> RAGGraphState: ]

["""使用大语言模型基于检索到的文档生成响应。""" ]

[question = state["question"] ][workflow.add_node("generate", generate_response_node) ]

 

[# 设置入口点 ]

[workflow.set_entry_point("retrieve") ]

 

[# 添加边（转换） ]

[workflow.add_edge("retrieve", "generate") ][workflow.add_edge("generate", END) ]

 

[# 编译图 ]

[app = workflow.compile() ]

 

[# --- 5. 运行检索增强生成应用 --- ]

[if __name__ == "__main__": ]

[print("\n--- Running RAG Query ---") ]

[query = "What did the president say about Justice Breyer" ]

[一览 ]

 

**是什么：** 大语言模型具备出色的文本生成能力，但从根本上受限于

其训练数据。这些知识是静态的，意味着它不包含实时信息或私有的、特定领域的数据。因此，它们的响应可能

过时、不准确，或缺乏专业任务所需的特定上下文。这一

差距限制了它们在需要当前且基于事实的答案的应用中的可靠性。

 

**为何：** 检索增强生成模式通过将大语言模型连接到外部知识源，提供了标准化解决方案。当收到查询时，

系统首先从指定的知识库检索相关信息片段。

然后将这些片段追加到原始提示，用及时且具体的上下文加以丰富。

随后将此增强后的提示发送给大语言模型，

![](images/000024.png)

![](images/000025.png)

● 智能体式检索增强生成超越了简单的信息检索，通过使用

智能体主动推理、验证并精炼外部知识，从而确保更准确、更可靠的答案。

● 实际应用涵盖企业搜索、客户支持、法律研究，

以及个性化推荐。

 

[结论 ]

 

总之，检索增强生成通过将大语言模型连接到外部、最新的

数据源，解决了其静态知识的核心局限。该过程首先检索相关信息片段，

然后增强用户的提示，使大语言模型能够生成更准确且具有上下文感知的响应。这得益于嵌入、语义搜索与向量数据库等基础技术，它们基于 [*3.* ]基于图的检索增强生成（GraphRAG），

<https://arxiv.org/abs/2501.00309>

[*4.* ]LangChain 与 LangGraph：Leonie Monigatti，「检索增强生成

（RAG）：从理论到 LangChain 实现」，

[[*https://medium.com/data-science/retrieval-augmented-generation-rag-fro*](https://medium.com/data-science/retrieval-augmented-generation-rag-from-theory-to-langchain-implementation-4e9bd5f6a4f2)]
