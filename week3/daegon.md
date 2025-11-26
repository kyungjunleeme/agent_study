# Building Agentic AI Systems

Chapter 3 : Essential Components of Intelligent Agents

## Knowledge Representation
* Semantic networks: 객체/개념을 Node로 하고 그들의 관계를 Edge로 표현하는 그래프
    * Useful for logic reasoning
* Frames: Data structure with a set of attribute(key)/value pairs
    * Useful in: Natural language processing, Expert systems, object-oriented programming, Computer Vision, Robotics
    * Useful for: knowledge-based reasoning decision-making
* Logic based representation: formal, mathematical route with symbolic logic (Wolfram Mathmatica?)
    * Useful in: Expert systems, Database systems, Automated reasoning(?), Legal/regulartory domains, Semantic web
    * Useful for: safety-critical domain, soundness, completeness
* Questions
    * Who defines frames? How to handle the data that does not fit the frames?

## Reasoning
* Deductive: 연역법, 일반에서 구체적으로
    * Useful in: 수학/기하학, 법, Software verification, Network routing
    * Useful With: other form of reasoning (Abduce/Deduce/Compare) 
* Inductive: 귀납법, 구체적 사실에서 일반적인 원리로
    * Useful in: 과학적 발견을 찾는 일, Machine Learning, 패턴 찾기, Data Mining, Natural lanauage acquisition.
    * Limitation: not perfect, just high probability
* Aductive: Find explanation, hypothesizes
    * Useful for: diagnostic domains and find root cause
    * Useful in: Medical diagnosis, Fault detection, Forensics/criminal investigation, AI planning, Scientific discovery
    * Resource intensive
* Seems to be used together, not separately

## Learning Mechanisms
* Supervised Learning: Training with input and expected output
    * Useful in: Image classification, Spam detection, Machine(Language) translation, Medical diagnosis
* Unsupervised Learning: Training with input only
    * Useful in: Customer segmentation, Anomaly detection, Topic modeling, Dimensionality reduction
* Reinforcement Learning: Rules, objective(s) with input/action generation
    * Useful in: Game playing, Robotics, Supply chain optimization, traffic control
* Transfer Learning: To exploit knowledge between different learning setting
    * Natural language processing (transfeering language models across domains)
    * Computer Vision ()
    * Recommendation systems ()

## Decision-making & Planning
* Utility Function: A function mapping states to a real number for preference. Mathematically, as long as comparable values will be fine. Will be used for decision-making and planning
    * Techniques to derive: preference elicitation (a series of questions to figure out utility function logic), inverse reinforcement learning, human feedback
* Planning Algorithms: Deriving sequences of actions to achieve a desirable state from a given state
    * Graph-based planning
        * Graph search
            * Algorithms: Depth-first search, breadth-first search, Dijkstra's algorithm (finding a shortest paths between all nodes)
        * Optimal path finding
            * Algorithms: Bellman-Ford and A* search
        * Limitation: contructing graph before decesion-making and exponential growth in graph size
    * Herristic search
        * Tradeoff between optimality and efficiency for finding a solution 
    * Monte Carlo tree search: Random simulations
        * Handle Uncertainty well
    * Hierarchical planning: hierarchical decomposition of a problem into sub-problems
        * Computational efficiency with reuse and a smaller size of problem
        * Knowledge representation at multiple levels of abstraction
        * Increased scalability
        * Not always optimal
    * Constraint satisfaction: a set of constraints with space reduction and optimization problem
        * A solver can be developed independent of problem representation.

## Enhancing Agent with Generative AI
### Major developments of AI for intelligent agents
* Data Augmentation: Generate training data with Gen AI
* Context Understanding
* Natural Language Processing: Impove Human interactions 
* Creative Problem Solving

### Where Generative AI can help for Intelligent Agent System
* Learning
* Knowledge representation
* Decision processes
* Context Understanding
* Feedback loop for continous learning
