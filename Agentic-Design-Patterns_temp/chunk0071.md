## [Chapter 4: Reflection, Chapter 5: Tool Use, Chapter 8: Memory Management, Appendix ][C ]

[● Latency Monitoring - Chapter 19: Evaluation and Monitoring ][● Learned Resource Allocation Policies - Chapter 16: Resource-Aware Optimization ][● Learning and Adaptation - Chapter 9: Learning and Adaptation ][● LLM-as-a-Judge - Chapter 19: Evaluation and Monitoring ][● LlamaIndex - Appendix C ]

[● LoRA (Low-Rank Adaptation) - Glossary ]

[● One-Shot Prompting - Appendix A ]

[● Online Learning - Chapter 9: Learning and Adaptation ][● OpenAI Deep Research API - Chapter 6: Planning ]

[● OpenEvolve - Chapter 9: Learning and Adaptation ]

[● OpenRouter - Chapter 16: Resource-Aware Optimization ][● Output Filtering/Post-processing - Chapter 18: Guardrails/Safety Patterns ]

 

[**P** ]

 

[● PAL (Program-Aided Language Models) - Chapter 17: Reasoning Techniques ][● Parallelization - Chapter 3: Parallelization ]

[● Parallelization & Distributed Computing Awareness - Chapter 16: Resource-Aware ]

[Optimization ]

[● Parameter-Efficient Fine-Tuning (PEFT) - Glossary ]

[● PEFT (Parameter-Efficient Fine-Tuning) - Glossary ]

[● Performance Tracking - Chapter 19: Evaluation and Monitoring ]

[● Reflection - Chapter 4: Reflection ]

[● Reinforcement Learning - Chapter 9: Learning and Adaptation ][● Reinforcement Learning from Human Feedback (RLHF) - Glossary ][● Reinforcement Learning with Verifiable Rewards (RLVR) - Chapter 17: Reasoning ]

[Techniques ]

[● Remote Agent - Chapter 15: Inter-Agent Communication (A2A) ][● Request/Response (Polling) - Chapter 15: Inter-Agent Communication (A2A) ][● Resource-Aware Optimization - Chapter 16: Resource-Aware Optimization ][● Retrieval-Augmented Generation (RAG) - Chapter 8: Memory Management, Chapter 14: ]

[Knowledge Retrieval (RAG), Appendix A ]

[● RLHF (Reinforcement Learning from Human Feedback) - Glossary ][● RLVR (Reinforcement Learning with Verifiable Rewards) - Chapter 17: Reasoning ]

[Techniques ]

[● RNN (Recurrent Neural Network) - Glossary ]

[● Role Prompting - Appendix A ]

[● System Prompting - Appendix A ]

 

[**T** ]

 

[● Task Evaluation - Chapter 20: Prioritization ]

[● Text Similarity - Chapter 14: Knowledge Retrieval (RAG) ][● Token Usage - Chapter 19: Evaluation and Monitoring ][● Tool Use - Chapter 5: Tool Use, Appendix A ]

[● Tool Use Restrictions - Chapter 18: Guardrails/Safety Patterns ][● ToT (Tree of Thoughts) - Chapter 17: Reasoning Techniques, Appendix A, Glossary ][● Transformers - Glossary ]

[● Tree of Thoughts (ToT) - Chapter 17: Reasoning Techniques, Appendix A, Glossary ]

 

[**U** ]

 

[● Unsupervised Learning - Chapter 9: Learning and Adaptation ]

[Prompt ]

[Below is the prompt that was utilized to create this index of terms. ]

 

[*do you read* ]

[*https://docs.google.com/document/d/1rsaK53T3Lg5KoGwvf8ukOUvbELRtH-V0LnOIFDxBryE/*] [*edit?tab=t.0 and all the related documents in the first page* ][*Please extract all the titles for each chapter. and print them.* ][*Then process the content of all the individual chapters, and create a detailed index used for* ][*publishing, a list of words or phrases (\'headings\') and associated pointers (\'locators\') to where* ][*useful material relating to that heading can be found in a document or collection of* ][*documents. I don\'t want a sample index. I want the full index, with 100 index terms* ]

 

[Gemini 2.5: Reasoning Steps ]I\'ve determined the user wants a chapter title list and comprehensive index from the Google Doc and related documents. Now I need to figure out the most effective method for this extraction and indexing process. I\'m exploring potential API functionalities to streamline this task, and will need to assess the best strategy for handling different document structures.

 

**3. Considering Tool Use**

 

I\'ve extracted the chapter URLs from the main document using a regular expression. Now, I\'m ready to utilize Workspaces to retrieve the actual content of each chapter. Once I have the text for each chapter, I\'ll proceed with indexing.

 

**Accessing chapter content:**

 

I\'ve successfully identified the URLs for each chapter from the main document, which I I\'ve extracted the chapter URLs and initiated a call to Workspaces. I\'m currently retrieving the content for each chapter. To ensure a smooth process, I\'m batching the calls to prevent any rate-limiting issues. This should enable me to efficiently compile the text needed for the index.

 

**Decoding User Request**

 

I\'ve determined the user\'s need. They require two primary deliverables: first, a comprehensive list of chapter titles extracted from Google Docs, and second, a detailed index containing a minimum of one hundred key terms. The process of extracting titles seems straightforward, while curating the index will involve more nuanced analysis.

 

**Extracting Titles and Indexing**

 

I\'ve successfully identified the user\'s need: extracting chapter titles from the provided alphabetically and noting their chapter locations. I am prepared to begin the indexing and extraction process.

[**Frequently Asked Questions: Agentic Design Patterns** ]

 

**What is an \"agentic design pattern\"?**[ An agentic design pattern is a reusable, high-level ][solution to a common problem encountered when building intelligent, autonomous systems ][(agents). These patterns provide a structured framework for designing agent behaviors, much ][like software design patterns do for traditional programming. They help developers build more ][robust, predictable, and effective AI agents. ]

 

**What is the main goal of this guide?**[ The guide aims to provide a practical, hands-on ][introduction to designing and building agentic systems. It moves beyond theoretical discussions ][to offer concrete architectural blueprints that developers can use to create agents capable of ][complex, goal-oriented behavior in a reliable way. ]

 
