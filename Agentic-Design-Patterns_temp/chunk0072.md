**Who is the intended audience for this guide?**[ This guide is written for AI developers, ][software engineers, and system architects who are building applications with large language ]**How does the \"Reflection\" pattern improve an agent\'s performance?**[ Reflection acts as a ][form of self-correction. After generating a response or completing a task, the agent can be ][prompted to review its work, check for errors, assess its quality against certain criteria, or ][consider alternative approaches. This iterative refinement process helps the agent produce ][more accurate, relevant, and high-quality results. ]

 

**What is the core idea of the Reflection pattern?**[ The Reflection pattern gives an agent the ][ability to step back and critique its own work. Instead of producing a final output in one go, the ][agent generates a draft and then \"reflects\" on it, identifying flaws, missing information, or areas ][for improvement. This self-correction process is key to enhancing the quality and accuracy of its ][responses. ]

 

**Why is simple \"prompt chaining\" not enough for high-quality output?**[ Simple prompt ][chaining (where the output of one prompt becomes the input for the next) is often too basic. The ][model might just rephrase its previous output without genuinely improving it. A true Reflection ][pattern requires a more structured critique, prompting the agent to analyze its work against ][objective, miss crucial steps, or fail to handle the output of one step as the input for the next. A ][plan provides a clear roadmap, ensuring all requirements of the original request are met in a ][logical order. ]

 

**What is a common way to implement the Planning pattern?**[ A common implementation is to ][have the agent first generate a list of steps in a structured format (like a JSON array or a ][numbered list). The system can then iterate through this list, executing each step one by one ][and feeding the result back to the agent to inform the next action. ]

 

**How does the agent handle errors or changes during execution?**[ A robust planning pattern ][allows for dynamic adjustments. If a step fails or the situation changes, the agent can be ][prompted to \"re-plan\" from the current state. It can analyze the error, modify the remaining ][steps, or even add new ones to overcome the obstacle. ]

 

**Does the user see the plan?**[ This is a design choice. In many cases, showing the plan to the ][user first for approval is a great practice. This aligns with the \"Human-in-the-Loop\" pattern, ]**What is the Human-in-the-Loop (HITL) pattern?**[ HITL is a pattern that integrates human ][oversight and interaction into the agent\'s workflow. Instead of being fully autonomous, the agent ][pauses at critical junctures to ask for human feedback, approval, clarification, or direction. ]

 

**Why is HITL important for agentic systems?**[ It\'s crucial for several reasons: ]

 

[● ]**Safety and Control:**[ For high-stakes tasks (e.g., financial transactions, sending official ]

[communications), HITL ensures a human verifies the agent\'s proposed actions before ][they are executed. ]

[● ]**Improving Quality:**[ Humans can provide corrections or nuanced feedback that the ]

[agent can use to improve its performance, especially in subjective or ambiguous tasks. ]

[● ]**Building Trust:**[ Users are more likely to trust and adopt an AI system that they can ]

[guide and supervise. ]

 

**At what points in a workflow should you include a human?**[ Common points for human ][intervention include: ]

**What is a common architecture for multi-agent systems?**[ A common architecture involves ][an ]**Orchestrator Agent**[ (sometimes called a \"manager\" or \"conductor\"). The orchestrator ][understands the overall goal, breaks it down, and delegates sub-tasks to the appropriate ][specialist agents. It then collects the results from the specialists and synthesizes them into a ][final output. ]

 

**How do the agents communicate with each other?**[ Communication is often managed by the ][orchestrator. For example, the orchestrator might pass the output of the \"researcher\" agent to ][the \"writer\" agent as context. A shared \"scratchpad\" or message bus where agents can post ][their findings is another common communication method. ]

 

**Why is evaluating an agent more difficult than evaluating a traditional software program?** [Traditional software has deterministic outputs (the same input always produces the same ][output). Agents, especially those using LLMs, are non-deterministic and their performance can ][be subjective. Evaluating them requires assessing the ][*quality*][ and ][*relevance*][ of their output, not ][just whether it\'s technically \"correct.\" ]

**What are the key components of a good system prompt for an agent?**[ A strong system ][prompt typically includes: ]

 

[● ]**Role and Goal:**[ Clearly define who the agent is and what its primary purpose is. ][● ]**Tool Definitions:**[ A list of available tools, their descriptions, and how to use them (e.g., ]

[in a specific function-calling format). ]

[● ]**Constraints and Rules:**[ Explicit instructions on what the agent ][*should not*][ do (e.g., \"Do ]

[not use tools without approval,\" \"Do not provide financial advice\"). ]

[● ]**Process Instructions:**[ Guidance on which patterns to use. For example, \"First, create a ]

[plan. Then, execute the plan step-by-step.\" ]

[● ]**Example Trajectories:**[ Providing a few examples of successful ]

[\"thought-action-observation\" loops can significantly improve the agent\'s reliability. ]

 

**What is \"prompt leakage\"?**[ Prompt leakage occurs when parts of the system prompt (like tool ][definitions or internal instructions) are inadvertently revealed in the agent\'s final response to the ][user. This can be confusing for the user and expose underlying implementation details. ]
