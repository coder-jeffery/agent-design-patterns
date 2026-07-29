[\"message\": f\"User login tracked. Total logins: ]

[{login_count}.\" ]

[} ]

 

[\# \-\-- Demonstration of Usage \-\-- ]

[\# In a real application, an LLM Agent would decide to call this ][tool. ]

[\# Here, we simulate a direct call for demonstration purposes. ]

 

[\# 1. Setup ]

[session_service = InMemorySessionService() ][app_name, user_id, session_id = \"state_app_tool\", \"user3\", ][\"session3\" ]

[\# and more robust. ]

 

This code demonstrates a tool-based approach for managing user session state in an

application. It defines a function *log_user_login*, which acts as a tool. This tool is responsible for updating the session state when a user logs in.

The function takes a ToolContext object, provided by the ADK, to access and modify

the session\'s state dictionary. Inside the tool, it increments a *user:login_count*, sets

the t*ask_status* to \"active\", records the *user:last_login_ts (timestamp)*, and adds a temporary flag temp:validation_needed.

 

The demonstration part of the code simulates how this tool would be used. It sets up

an in-memory session service and creates an initial session with some predefined state. A ToolContext is then manually created to mimic the environment in which the for agents to retain information across multiple interactions or access external data,

long-term knowledge management is necessary. This is facilitated by the MemoryService.

 

[\# Example: Using InMemoryMemoryService ]

[\# This is suitable for local development and testing where data ][\# persistence across application restarts is not required. ][\# Memory content is lost when the app stops. ][from google.adk.memory import InMemoryMemoryService ][memory_service = InMemoryMemoryService() ]

 

Session and State can be conceptualized as short-term memory for a single chat

session, whereas the Long-Term Knowledge managed by the MemoryService

functions as a persistent and searchable repository. This repository may contain

[\# Optional configuration for retrieval behavior ][SIMILARITY_TOP_K = 5 \# Number of top results to retrieve ][VECTOR_DISTANCE_THRESHOLD = 0.7 \# Threshold for vector similarity ]

 

 

[memory_service = VertexAiRagMemoryService( ]

[rag_corpus=RAG_CORPUS_RESOURCE_NAME, ]

[similarity_top_k=SIMILARITY_TOP_K, ]

[vector_distance_threshold=VECTOR_DISTANCE_THRESHOLD ][) ]

[\# When using this service, methods like add_session_to_memory ][\# and search_memory will interact with the specified Vertex AI ][\# RAG Corpus. ]

 

[Hands-on code: Memory Management in LangChain ]

**ChatMessageHistory: Manual Memory Management.** For direct and simple control over a conversation\'s history outside of a formal chain, the ChatMessageHistory class

 

is ideal. It allows for the manual tracking of dialogue exchanges.

 

[from langchain.memory import ChatMessageHistory ]

 

[\# Initialize the history object ]

[history = ChatMessageHistory() ]

 

[\# Add user and AI messages ]

[history.add_user_message(\"I\'m heading to New York next week.\") ][history.add_ai_message(\"Great! It\'s a fantastic city.\") ]

 

[\# Access the list of messages ]Integrating this memory into an LLMChain allows the model to access the

conversation\'s history and provide contextually relevant responses

 

[from langchain_openai import OpenAI ]

[from langchain.chains import LLMChain ]

[from langchain.prompts import PromptTemplate ][from langchain.memory import ConversationBufferMemory ]

 

[\# 1. Define LLM and Prompt ]

[llm = OpenAI(temperature=0) ]

[template = \"\"\"You are a helpful travel agent. ]

 

[Previous conversation: ]

[{history} ]

[SystemMessagePromptTemplate, ]

[HumanMessagePromptTemplate, ]

[) ]

 

[\# 1. Define Chat Model and Prompt ]

[llm = ChatOpenAI() ]

[prompt = ChatPromptTemplate( ]

[messages=\[ ]

[SystemMessagePromptTemplate.from_template(\"You are a friendly ][assistant.\"), ]

[MessagesPlaceholder(variable_name=\"chat_history\"), ]

[HumanMessagePromptTemplate.from_template(\"{question}\") ]

[\] ]

[) ]

 

[\# 2. Configure Memory ]

few-shot example prompting, where an agent learns from past successful

interaction sequences to perform tasks correctly.

● **Procedural Memory: Remembering Rules:** This is the memory of how to

perform tasks---the agent\'s core instructions and behaviors, often contained in

its system prompt. It\'s common for agents to modify their own prompts to

adapt and improve. An effective technique is \"Reflection,\" where an agent is prompted with its current instructions and recent interactions, then asked to

refine its own instructions.

 

Below is pseudo-code demonstrating how an agent might use reflection to update its procedural memory stored in a LangGraph BaseStore

 

[\# Node that updates the agent\'s instructions ]

LangGraph stores long-term memories as JSON documents in a store. Each memory is organized under a custom namespace (like a folder) and a distinct key (like a

 

filename). This hierarchical structure allows for easy organization and retrieval of

information. The following code demonstrates how to use InMemoryStore to put, get,

and search for memories.

 

[from langgraph.store.memory import InMemoryStore ]

 

[\# A placeholder for a real embedding function ][def embed(texts: list\[str\]) -\> list\[list\[float\]\]: ]

[\# In a real application, use a proper embedding model ]

[namespace, ]

[filter={\"my-key\": \"my-value\"}, ]

[query=\"language preferences\" ]

[) ]

[print(\"Search Results:\", items) ]

 

[Vertex Memory Bank ]

 

Memory Bank, a managed service in the Vertex AI Agent Engine, provides agents with persistent, long-term memory. The service uses Gemini models to asynchronously

analyze conversation histories to extract key facts and user preferences.

 

This information is stored persistently, organized by a defined scope like user ID, and

Memory Bank offers seamless integration with the Google ADK, providing an

 

immediate out-of-the-box experience. For users of other agent frameworks, such as LangGraph and CrewAI, Memory Bank also offers support through direct API calls.

Online code examples demonstrating these integrations are readily available for

interested readers.

 

[At a Glance ]

 
