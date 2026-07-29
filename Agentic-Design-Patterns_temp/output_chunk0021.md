## [第 8 章：记忆管理 ]

 

有效的记忆管理对智能体保留信息至关重要。

智能体与人类一样，需要不同类型的记忆才能高效运行。本章深入探讨记忆管理，具体面向智能体的即时

（短期）与持久（长期）记忆需求。

 

在智能体系统中，记忆指智能体保留并利用来自过往交互、观察与学习经验的

信息的能力。这一能力使智能体能够做出知情决策、维持对话上下文，并随时间

不断改进。智能体记忆通常分为两大类：

 

● **短期记忆（上下文记忆）：** 类似于工作记忆，它

保存当前正在处理或最近访问的信息。对智能体而言

与当前交互相关的知识。

 

[实际应用与用例 ]

 

记忆管理对智能体跟踪信息并随时间智能运作至关重要。这对于智能体超越基本的问答

能力必不可少。应用包括：

 

● **聊天机器人与对话式 AI：** 维持对话流畅依赖

短期记忆。聊天机器人需要记住先前的用户输入，才能给出连贯回答。长期记忆使聊天机器人能够回忆用户

偏好、过往问题或先前讨论，从而提供个性化且

持续的交互。

● **任务导向智能体：** 管理多步骤任务的智能体需要短期 [动手代码：Google 中的记忆管理 ]

 

[Agent Developer Kit（ADK） ]

 

Google Agent Developer Kit（ADK）提供了一种结构化方法来管理

上下文与记忆，并包含可实际应用的组件。扎实掌握

ADK 的 Session、State 与 Memory，对于构建需要保留信息的智能体至关重要。

 

正如人际交流一样，智能体需要回忆先前交流的能力，

才能进行连贯自然的对话。ADK 通过三个核心概念及其相关服务，简化了

上下文管理。

 

每一次与智能体的交互都可以视为一个独特的对话线程。

智能体可能需要访问更早交互中的数据。ADK 将其结构化为 [Session：跟踪每一次聊天 ]

 

ADK 中的 Session 对象用于跟踪和管理各个聊天线程。在与智能体发起对话时，SessionService 会生成一个

Session 对象，表示为 \`google.adk.sessions.Session\`。该对象

封装与特定对话线程相关的全部数据，包括唯一

标识符（id、app_name、user_id）、以 Event 对象形式按时间顺序记录的事件、用于存放会话专用临时数据的存储区（称为 state），以及指示

上次更新时间的时间戳（last_update_time）。开发者通常通过

SessionService 间接与 Session 对象交互。SessionService 负责

管理对话会话的生命周期，包括发起新会话、恢复先前会话、记录会话活动

（包括状态更新）、识别活跃会话，以及管理

会话数据的移除。ADK 提供多种具有不同特性的 SessionService 实现

此外，还有 VertexAiSessionService，它利用 Vertex AI 基础设施在

 

Google Cloud 上实现可扩展的生产部署。

 

[\# 示例：使用 VertexAiSessionService ]

[\# 适用于 Google Cloud Platform 上的可扩展生产环境，][借助 ]

[\# Vertex AI 基础设施进行会话管理。][\# 需要：pip install google-adk\[vertexai\] 以及 GCP ][配置/认证 ]

[from google.adk.sessions import VertexAiSessionService ]事件并更新存储中的状态。随后 Session 等待下一条消息。

理想情况下，在交互结束时使用 delete_session 方法终止会话。这一过程说明了 SessionService 如何通过管理

Session 专用的历史记录与临时数据来维持连续性。

 

[State：会话的草稿本 ]

 

在 ADK 中，每个代表聊天线程的 Session 都包含一个 state 组件，类似于智能体在该特定

对话期间的临时工作记忆。session.events 记录完整的聊天历史，而 session.state 则存储

并更新与当前活跃聊天相关的动态数据点。

 

从根本上说，session.state 以字典方式运行，以键值对存储数据。其核心功能是使智能体能够保留并管理对

追加事件时将响应保存到状态中至关重要的细节。让我们看一个通过 output_key

演示状态更新的代码示例。

 

[\# 从 Google Agent Developer Kit ][（ADK）导入必要的类 ]

[from google.adk.agents import LlmAgent ]

[from google.adk.sessions import InMemorySessionService, Session ][from google.adk.runners import Runner ]

[from google.genai.types import Content, Part ]

 

[\# 定义带有 output_key 的 LlmAgent。 ]

[greeting_agent = LlmAgent( ]

[name=\"Greeter\", ]

[model=\"gemini-2.0-flash\", ]

[instruction=\"Generate a short, friendly greeting.\", ]

[output_key=\"last_greeting\" ]

[处理所有事件。 ]

[updated_session = session_service.get_session(app_name, user_id, ][session_id) ]

[print(f\"\\nState after agent run: {updated_session.state}\") ]

 

在幕后，Runner 会识别你的 output_key，并在调用 append_event 时自动创建带有 state_delta 的必要操作。

 

[2. ]**标准方式：使用 EventActions.state_delta（用于更复杂的**

**更新）：** 当你需要做更复杂的事情时——例如一次更新

多个键、保存非纯文本内容、针对 user: 或 app: 等特定作用域，或进行与智能体最终文本回复

无关的更新——你需要手动构建一个状态变更字典（即 state_delta），并将其

包含在你所追加的 Event 的 EventActions 中。让我们看一个

[return { ]

[\"status\": \"success\", ]
