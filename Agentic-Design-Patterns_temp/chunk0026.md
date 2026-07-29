## [Chapter 10: Model Context Protocol ]

 

To enable LLMs to function effectively as agents, their capabilities must extend

beyond multimodal generation. Interaction with the external environment is necessary, including access to current data, utilization of external software, and execution of

specific operational tasks. The Model Context Protocol (MCP) addresses this need by

providing a standardized interface for LLMs to interface with external resources. This

protocol serves as a key mechanism to facilitate consistent and predictable integration.

 

[MCP Pattern Overview ]

 

Imagine a universal adapter that allows any LLM to plug into any external system, Furthermore, MCP can wrap an API whose input or output is still not inherently

understandable by the agent. An API is only useful if its data format is agent-friendly, a guarantee that MCP itself does not enforce. For instance, creating an MCP server

for a document store that returns files as PDFs is mostly useless if the consuming

agent cannot parse PDF content. The better approach would be to first create an API

that returns a textual version of the document, such as Markdown, which the agent can actually read and process. This demonstrates that developers must consider not

just the connection, but the nature of the data being exchanged to ensure true

compatibility.

 

[MCP vs. Tool Function Calling ]

 

The Model Context Protocol (MCP) and tool function calling are distinct mechanisms Here\'s a breakdown of the fundamental distinctions between MCP and tool function

calling:

 

**Feature** **Tool Function Calling** **Model Context Protocol (MCP)**

 

**Standardization** Proprietary and [An open, standardized protocol, ]

vendor-specific. The format promoting interoperability and implementation differ [between different LLMs and tools. ]

across LLM providers.

 

**Scope** A direct mechanism for an A broader framework for how

LLM to request the [LLMs and external tools discover ]

execution of a specific, and communicate with each In short, function calling provides direct access to a few specific functions, while MCP

is the standardized communication framework that lets LLMs discover and use a vast range of external resources. For simple applications, specific tools are enough; for

complex, interconnected AI systems that need to adapt, a universal standard like MCP

is essential.

 

[Additional considerations for MCP ]

 

While MCP presents a powerful framework, a thorough evaluation requires considering several crucial aspects that influence its suitability for a given use case.

Let\'s see some aspects in more details:

 

● **Tool vs. Resource vs. Prompt**: It\'s important to understand the specific roles

of these components. A resource is static data (e.g., a PDF file, a database

architecture allows for shared, scalable access to common tools across an

organization.

● **On-demand vs. Batch**: MCP can support both on-demand, interactive

sessions and larger-scale batch processing. The choice depends on the

application, from a real-time conversational agent needing immediate tool

access to a data analysis pipeline that processes records in batches.

● **Transportation Mechanism**: The protocol also defines the underlying

transport layers for communication. For local interactions, it uses JSON-RPC

over STDIO (standard input/output) for efficient inter-process communication.

For remote connections, it leverages web-friendly protocols like Streamable HTTP and Server-Sent Events (SSE) to enable persistent and efficient

client-server communication.

 

The Model Context Protocol uses a client-server model to standardize information

2\. **Request Formulation**: The LLM determines that it needs to use one of the

discovered tools. For instance, it decides to send an email. It formulates a request, specifying the tool to use (send_email) and the necessary parameters

(recipient, subject, body).

3\. **Client Communication**: The MCP Client takes the LLM\'s formulated request

and sends it as a standardized call to the appropriate MCP Server.

4\. **Server Execution**: The MCP Server receives the request. It authenticates the

client, validates the request, and then executes the specified action by

interfacing with the underlying software (e.g., calling the send() function of an

email API).

5\. **Response and Context Update**: After execution, the MCP Server sends a

standardized response back to the MCP Client. This response indicates

whether the action was successful and includes any relevant output (e.g., a

confirmation ID for the sent email). The client then passes this result back to

traditional search tool returning an entire document, an agent can analyze the

text and extract the precise clause, figure, or statement that directly answers a user\'s complex question.

[● ]**Custom Tool Development:** Developers can build custom tools and expose them

via an MCP server (e.g., using FastMCP). This allows specialized internal functions

or proprietary systems to be made available to LLMs and other agents in a standardized, easily consumable format, without needing to modify the LLM

directly.

[● ]**Standardized LLM-to-Application Communication:** MCP ensures a consistent

communication layer between LLMs and the applications they interact with. This reduces integration overhead, promotes interoperability between different LLM

providers and host applications, and simplifies the development of complex

agentic systems.

[● ]**Complex Workflow Orchestration:** By combining various MCP-exposed tools

[Agent Setup with MCPToolset ]

 

 

To configure an agent for file system interaction, an \`agent.py\` file must be created (e.g., at \`./adk_agent_samples/mcp_agent/agent.py\`). The \`MCPToolset\` is

instantiated within the \`tools\` list of the \`LlmAgent\` object. It is crucial to replace

\`\"/path/to/your/folder\"\` in the \`args\` list with the absolute path to a directory on the

local system that the MCP server can access. This directory will be the root for the file system operations performed by the agent.

 

[import os ]
