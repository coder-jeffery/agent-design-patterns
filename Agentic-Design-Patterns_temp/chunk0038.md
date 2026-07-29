## [Chapter 16: Resource-Aware ]

 

[Optimization ]

 

Resource-Aware Optimization enables intelligent agents to dynamically monitor and

manage computational, temporal, and financial resources during operation. This differs from simple planning, which primarily focuses on action sequencing.

Resource-Aware Optimization requires agents to make decisions regarding action

execution to achieve goals within specified resource budgets or to optimize efficiency.

This involves choosing between more accurate but expensive models and faster, lower-cost ones, or deciding whether to allocate additional compute for a more

refined response versus returning a quicker, less detailed answer.

● **Data Usage Management:** An agent opting for summarized data retrieval

instead of full dataset downloads to save bandwidth or storage.

● **Adaptive Task Allocation:** In multi-agent systems, agents self-assign tasks

based on their current computational load or available time.

 

[Hands-On Code Example ]

 

An intelligent system for answering user questions can assess the difficulty of each question. For simple queries, it utilizes a cost-effective language model such as

Gemini Flash. For complex inquiries, a more powerful, but expensive, language model

(like Gemini Pro) is considered. The decision to use the more powerful model also

depends on resource availability, specifically budget and time constraints. This system dynamically selects appropriate models.

[\# Conceptual Python-like structure, not runnable code ]

 

 

[from google.adk.agents import Agent ]

[\# from google.adk.models.lite_llm import LiteLlm \# If using models ][not directly supported by ADK\'s default Agent ]

 

[\# Agent using the more expensive Gemini Pro 2.5 ][gemini_pro_agent = Agent( ]

[name=\"GeminiProAgent\", ]

[model=\"gemini-2.5-pro\", \# Placeholder for actual model name if ][different ]

[description=\"A highly capable agent for complex queries.\", ]

[instruction=\"You are an expert assistant for complex ][problem-solving.\" ]

[\# Conceptual Python-like structure, not runnable code ]

 

 

[from google.adk.agents import Agent, BaseAgent ][from google.adk.events import Event ]

[from google.adk.agents.invocation_context import InvocationContext ][import asyncio ]

 

[class QueryRouterAgent(BaseAgent): ]

[name: str = \"QueryRouter\" ]

[description: str = \"Routes user queries to the appropriate LLM ][agent based on complexity.\" ]

 

[async def \_run_async_impl(self, context: InvocationContext) -\> ][AsyncGenerator\[Event, None\]: ]quality. It also systematically assesses responses for performance monitoring,

tracking metrics like accuracy and relevance, which are used for optimization.

 

Additionally, its feedback can signal reinforcement learning or fine-tuning; consistent

identification of inadequate Flash model responses, for instance, can refine the router

agent\'s logic. While not directly managing the budget, the Critique Agent contributes

to indirect budget management by identifying suboptimal routing choices, such as directing simple queries to a Pro model or complex queries to a Flash model, which

leads to poor results. This informs adjustments that improve resource allocation and

cost savings.

 

The Critique Agent can be configured to review either only the generated text from the answering agent or both the original query and the generated text, enabling a

comprehensive evaluation of the response\'s alignment with the initial question. prompt should also encourage the identification of both strengths and weaknesses,

and it must guide the agent on how to structure and present its feedback.

 

[Hands-On Code with OpenAI ]

 

This system uses a resource-aware optimization strategy to handle user queries

efficiently. It first classifies each query into one of three categories to determine the

most appropriate and cost-effective processing pathway. This approach avoids

wasting computational resources on simple requests while ensuring complex queries get the necessary attention. The three categories are:

 

● simple: For straightforward questions that can be answered directly without

complex reasoning or external data.

[\"Please set OPENAI_API_KEY, GOOGLE_CUSTOM_SEARCH_API_KEY, and ][GOOGLE_CSE_ID in your .env file.\" ]

[) ]

 

[client = OpenAI(api_key=OPENAI_API_KEY) ]

 

[\# \-\-- Step 1: Classify the Prompt \-\-- ]

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

 

[\# \-\-- Step 4: Combined Router \-\-- ]

[def handle_prompt(prompt: str) -\> dict: ]

[classification_result = classify_prompt(prompt) ]

 

[\# print(\"\\n] [🔍] [\# Remove or comment out the next line to avoid duplicate printing ][ Classification Result:\", classification_result) ]then generates the final response, selecting an appropriate OpenAI model based on

the classification. For internet search queries, the search results are provided as context to the model. The main handle_prompt function orchestrates this workflow,

calling the classification and search (if needed) functions before generating the

response. It returns the classification, the model used, and the generated answer. This

system efficiently directs different types of queries to optimized methods for a better response.

 

[Hands-On Code Example (OpenRouter) ]

 
