## [Chapter 2: Routing ]

 

[Routing Pattern Overview ]

 

While sequential processing via prompt chaining is a foundational technique for

executing deterministic, linear workflows with language models, its applicability is

limited in scenarios requiring adaptive responses. Real-world agentic systems must often arbitrate between multiple potential actions based on contingent factors, such

as the state of the environment, user input, or the outcome of a preceding operation.

This capacity for dynamic decision-making, which governs the flow of control to

different specialized functions, tools, or sub-processes, is achieved through a mechanism known as routing.

 

Routing introduces conditional logic into an agent\'s operational framework, enabling a

user query and output only the category: \'Order Status\', \'Product Info\', \'Technical

Support\', or \'Other\'.\" The agentic system then reads this output and directs the workflow accordingly.

[● ]**Embedding-based Routing:** The input query can be converted into a vector

embedding (see RAG, Chapter 14). This embedding is then compared to

embeddings representing different routes or capabilities. The query is routed to the route whose embedding is most similar. This is useful for semantic routing,

where the decision is based on the meaning of the input rather than just

keywords.

[● ]**Rule-based Routing:** This involves using predefined rules or logic (e.g., if-else

statements, switch cases) based on keywords, patterns, or structured data

extracted from the input. This can be faster and more deterministic than

LLM-based routing, but is less flexible for handling nuanced or novel inputs.

● **Machine Learning Model-Based Routing**: it employs a discriminative model, the functions or model-based evaluations that dictate the transitions between nodes

in the computational graph.

 

The implementation of routing enables a system to move beyond deterministic

sequential processing. It facilitates the development of more adaptive execution flows

that can respond dynamically and appropriately to a wider range of inputs and state

changes.

 

[Practical Applications & Use Cases ]

 

The routing pattern is a critical control mechanism in the design of adaptive agentic

systems, enabling them to dynamically alter their execution path in response to

variable inputs and internal states. Its utility spans multiple domains by providing a necessary layer of conditional logic. decisions about the most effective method for accomplishing a task under changing

conditions.

 

[Hands-On Code Example (LangChain) ]

 

Implementing routing in code involves defining the possible paths and the logic that

decides which path to take. Frameworks like LangChain and LangGraph provide

specific components and structures for this. LangGraph\'s state-based graph structure is particularly intuitive for visualizing and implementing routing logic.

 

This code demonstrates a simple agent-like system using LangChain and Google\'s

Generative AI. It sets up a \"coordinator\" that routes user requests to different

simulated \"sub-agent\" handlers based on the request\'s intent (booking, information, or unclear). The system uses a language model to classify the request and then [temperature=0) ]

[print(f\"Language model initialized: {llm.model}\") ][except Exception as e: ]

[print(f\"Error initializing language model: {e}\") ]

[llm = None ]

 

[\# \-\-- Define Simulated Sub-Agent Handlers (equivalent to ADK ][sub_agents) \-\-- ]

 

[def booking_handler(request: str) -\> str: ]

[\"\"\"Simulates the Booking Agent handling a request.\"\"\" ]

[print(\"\\n\-\-- DELEGATING TO BOOKING HANDLER \-\--\") ]

[return f\"Booking Handler processed request: \'{request}\'. Result: ][Simulated booking action.\" ]

 

[def info_handler(request: str) -\> str: ][based on sub_agents) \-\-- ]

[\# Use RunnableBranch to route based on the router chain\'s output. ]

 

[\# Define the branches for the RunnableBranch ][branches = { ]

[\"booker\": RunnablePassthrough.assign(output=lambda x: ][booking_handler(x\[\'request\'\]\[\'request\'\])), ]

[\"info\": RunnablePassthrough.assign(output=lambda x: ][info_handler(x\[\'request\'\]\[\'request\'\])), ]

[\"unclear\": RunnablePassthrough.assign(output=lambda x: ][unclear_handler(x\[\'request\'\]\[\'request\'\])), ][} ]

 

[\# Create the RunnableBranch. It takes the output of the router chain ][\# and routes the original input (\'request\') to the corresponding ][handler. ]

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

 

As mentioned, this Python code constructs a simple agent-like system using the routing within the ADK paradigm is typically implemented by defining a discrete set of

\"tools\" that represent the agent\'s functions. The selection of the appropriate tool in response to a user query is managed by the framework\'s internal logic, which

leverages an underlying model to match user intent to the correct functional handler.

 

This Python code demonstrates an example of an Agent Development Kit (ADK)

application using Google\'s ADK library. It sets up a \"Coordinator\" agent that routes user requests to specialized sub-agents (\"Booker\" for bookings and \"Info\" for general

information) based on defined instructions. The sub-agents then use specific tools to

simulate handling the requests, showcasing a basic delegation pattern within an agent

system

 

[\# Copyright (c) 2025 Marco Fago ]

[\# ]

[request: The user\'s question. ]

[Returns: ]

[A message indicating the information request was handled. ]

[\"\"\" ]
