## [Chapter 8: Memory Management ]

 

Effective memory management is crucial for intelligent agents to retain information.

Agents require different types of memory, much like humans, to operate efficiently. This chapter delves into memory management, specifically addressing the immediate

(short-term) and persistent (long-term) memory requirements of agents.

 

In agent systems, memory refers to an agent\'s ability to retain and utilize information

from past interactions, observations, and learning experiences. This capability allows agents to make informed decisions, maintain conversational context, and improve over

time. Agent memory is generally categorized into two main types:

 

● **Short-Term Memory (Contextual Memory):** Similar to working memory, this

holds information currently being processed or recently accessed. For agents

knowledge with the current interaction.

 

[Practical Applications & Use Cases ]

 

Memory management is vital for agents to track information and perform intelligently over time. This is essential for agents to surpass basic question-answering

capabilities. Applications include:

 

● **Chatbots and Conversational AI:** Maintaining conversation flow relies on

short-term memory. Chatbots require remembering prior user inputs to provide coherent responses. Long-term memory enables chatbots to recall user

preferences, past issues, or prior discussions, offering personalized and

continuous interactions.

● **Task-Oriented Agents:** Agents managing multi-step tasks need short-term [Hands-On Code: Memory Management in Google ]

 

[Agent Developer Kit (ADK) ]

 

The Google Agent Developer Kit (ADK) offers a structured method for managing

context and memory, including components for practical application. A solid grasp of

ADK\'s Session, State, and Memory is vital for building agents that need to retain information.

 

Just as in human interactions, agents require the ability to recall previous exchanges

to conduct coherent and natural conversations. ADK simplifies context management

through three core concepts and their associated services.

 

Every interaction with an agent can be considered a unique conversation thread.

Agents might need to access data from earlier interactions. ADK structures this as [Session: Keeping Track of Each Chat ]

 

A Session object in ADK is designed to track and manage individual chat threads. Upon initiation of a conversation with an agent, the SessionService generates a

Session object, represented as \`google.adk.sessions.Session\`. This object

encapsulates all data relevant to a specific conversation thread, including unique

identifiers (id, app_name, user_id), a chronological record of events as Event objects, a storage area for session-specific temporary data known as state, and a timestamp

indicating the last update (last_update_time). Developers typically interact with

Session objects indirectly through the SessionService. The SessionService is

responsible for managing the lifecycle of conversation sessions, which includes initiating new sessions, resuming previous sessions, recording session activity

(including state updates), identifying active sessions, and managing the removal of

session data. The ADK provides several SessionService implementations with varying

Besides, there\'s VertexAiSessionService which uses Vertex AI infrastructure for

 

scalable production on Google Cloud.

 

[\# Example: Using VertexAiSessionService ]

[\# This is suitable for scalable production on Google Cloud Platform, ][leveraging ]

[\# Vertex AI infrastructure for session management. ][\# Requires: pip install google-adk\[vertexai\] and GCP ][setup/authentication ]

[from google.adk.sessions import VertexAiSessionService ]event and updates the state in storage. The Session then awaits the next message.

Ideally, the delete_session method is employed to terminate the session when the interaction concludes. This process illustrates how the SessionService maintains

continuity by managing the Session-specific history and temporary data.

 

[State: The Session\'s Scratchpad ]

 

In the ADK, each Session, representing a chat thread, includes a state component akin to an agent\'s temporary working memory for the duration of that specific

conversation. While session.events logs the entire chat history, session.state stores

and updates dynamic data points relevant to the active chat.

 

Fundamentally, session.state operates as a dictionary, storing data as key-value pairs. Its core function is to enable the agent to retain and manage details essential for

save the response to the state when it appends the event. Let\'s look at a code

example demonstrating state update via output_key.

 

[\# Import necessary classes from the Google Agent Developer Kit ][(ADK) ]

[from google.adk.agents import LlmAgent ]

[from google.adk.sessions import InMemorySessionService, Session ][from google.adk.runners import Runner ]

[from google.genai.types import Content, Part ]

 

[\# Define an LlmAgent with an output_key. ]

[greeting_agent = LlmAgent( ]

[name=\"Greeter\", ]

[model=\"gemini-2.0-flash\", ]

[instruction=\"Generate a short, friendly greeting.\", ]

[output_key=\"last_greeting\" ]

[processing all events. ]

[updated_session = session_service.get_session(app_name, user_id, ][session_id) ]

[print(f\"\\nState after agent run: {updated_session.state}\") ]

 

Behind the scenes, the Runner sees your output_key and automatically creates the necessary actions with a state_delta when it calls append_event.

 

[2. ]**The Standard Way: Using EventActions.state_delta (for More Complicated**

**Updates):** For times when you need to do more complex things -- like updating

several keys at once, saving things that aren\'t just text, targeting specific scopes like user: or app:, or making updates that aren\'t tied to the agent\'s final text reply

-- you\'ll manually build a dictionary of your state changes (the state_delta) and

include it within the EventActions of the Event you\'re appending. Let\'s look at one

[return { ]

[\"status\": \"success\", ]
