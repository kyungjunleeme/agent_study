# Building Agentic AI Systems

## Chapter 6 : Exploring the Coordinator, Worker and Delegator Approach

This chapter introduces the CWD model, a comprehensive framework designed to facilitate 
the development of multi-agent systems and its adaption in LLM-based AI agent development.

* Coordinators: manage tasks, resource and the overall workflow of the system
* Workers: specialized for carrying out specific tasks/functions
* Delegators: intermediaries between coordinators and workers, responsible for workload assignment

### Key Principles
* Separation of concerns
* Hierarchical organization
* Information flow and feedback loops
* Adaptability and resilience
    * Dynamic resource allocation
    * Fault tolerance through redundancy
    * Load Balancing across agents
    * Runtime role reassignment

### Interaction between Agents
* Communication: well-defined protocols. 
    * FIPA Agent Communication Language (ACL)
        * Speech Act Theory: FIPA ACL treats messages as intentional actions (communicative acts) with effects on the receiver's mental state, not just data.
        * Message Structure: Each message includes headers (sender, receiver, protocol, conversation ID) and a content part (the information or action, described using a content language like SL or XML).
        * Performatives (Communicative Acts): Specific verbs defining the intent, such as inform, request, query-if, subscribe, agree, refuse, cfp (Call For Proposals).
        * Interaction Protocols: Predefined sequences of ACL messages (e.g., a request followed by an inform or refuse) to manage conversations and achieve goals. 
* Coordination 
* Negotiation and conflict resolution
* Knowledge sharing

### Implementing the CWD approach in generative AI systems
Behaviors and interactions are primarily controlled by prompts and interaction patterns.
* System prompts
    * Role definition and scope of responsibilities
    * Contraints and operational boundaries
    * Communication protocol with other agents
    * Decision-making framework specific to their role
* Instruction Formatting
    * Input structuring
    * Output templates
    * Communication protocols
* Interaction Patterns
    * Message passing
    * State management
    * Feedback loops
