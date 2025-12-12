# Building Agentic AI Systems

## Chapter 5 : Enabling Tool Use and Planning in Agents

Tool Usage: LLM agent's capability of leveraging **external** resources or instrumentation
to **augement** the agent's inherent functionality and decision-making process.

### Tool vs Function calling
* Function call: structured calls to pre-defined functions, internal tasks e.g. database lookup and calculation. 
* Tool call: call to external APIs, services or system

### On Tools/functions
* Invoking
    * Which tool/function to use
    * Description of Input parameters
    * Format of input parameters
* Tool definition (Clear Description)
    * The purpose (what it is expected to do)
    * Inputs from Agent (Agent Controller) (description and format)
        * Required
        * Optional
    * Outputs to Agent (Agent Controller)
* Specification
    * Docstrings (with framework like LangChain)
    * Direct LLM integration
* **Things to keep in mind**
    * Model dependent (tools are provided by LLM, not externally)

### Types of Tools
* Application programming interfaces(APIs)
    * Example: 
        * Commercial: [Serpapi](https://serpapi.com/) (Web Search), [OpenWeatherMap](https://openweathermap.org/api)
        * Free: DuckDuckGoSearchTool from smolagents
* Database tools
* Utility functions: locally, specialized tasks
* Integration tools: bridge between different platforms/services
* Hardware interface tools: physical devices/system

### Aspects to be considered when tools are used
* Tool composition and chaining
* Tool selection and decision-making: capabilities, reliability, performance and cost
* Error handling & fallbacks
* Tool state management
* Tool updates/versioning
* Tool security and access control

### Planning Algorithm
* Less Practical Planning Algorithms
    * STRIPS (Standard Research Institute Problem Solvers)L logical predicates
    * A* planning: path finding algorithm requires mathematically defined paths and cost functiong.
    * GraphPlan: using layered graph structures for action and effects
    * MCTS (Monte Carlo Tree Search): Costly due to too many calls to LLM (sampling) and the space is large
* Moderately Practical Planning Algorithms
    * FF (Fast Forward): a heuristic search with simple problem specification, goal oriented
* Most Practical Planning Algorithms
    * LLM-based Planning: Using LLM with natural language description
    * HTN Planning: Breaking (abstract) complex tasks into simpler (concrete) subtasks down to (directly executable) primitive tasks.

### AI Agent with tools and reasoning
* Modern LLMs are trained to understand tool descriptions, purposes, appropriate usage contexts
* Not all LLMs are equally capable of effective tool reasoning

### Implementation Frameworks
* CrewAI
* AutoGen
* LangGraph
