# automata-sim#

**HW:** Potential technical solutions

## 1\. Team Identification

| Team Member Name |
| :---- |
| Leonte Luca |
| Tofan Anastasia |
| Pirvan Ana Maria |
| Zuzu Laura Ioana |

&nbsp;

For collaboration we’ll use GitHub and Trello.

## 2\. General Architecture and Technologies

Both the backend and the frontend will be developed entirely in Python. We will use some of the following libraries:

1. NumPy  
2. PyTorch  
3. Streamlit

The cellular automaton can be described in JSON format. The JSON file will then be used in a simulator that will parse it and generate the next states. The data provided by the simulator will be then used to train a RN model or for smaller input will be used to answer some of the 5 questions. Based on the dataset RN models will be trained to answer the questions.&nbsp;

Using this approach we can easily implement/add new cellular automaton described in natural language.

## 3\. Proposed Technical Solutions by Component

### A. Generalized Automaton Encoding

To cover a wide range of cellular automata (1D/2D, deterministic, probabilistic, or agent-based), any validated description will be translated into a JSON file.

* **Initial state.**  
* **Grid dimensions and topology:** 1D or 2D representation.  
* **Set of states.**  
* **Neighborhood configuration:** The arrangement of adjacent cells that influence the current state (e.g., 4 neighbors, 8 neighbors, left-right).  
* **Transition rules:** Logical conditions and others.

### B. Hybrid Approach for Answering Queries (Simulation \+ AI)

Because step-by-step simulation becomes computationally inefficient for very large values of $N$, the system will employ a hybrid strategy:

1. **Deterministic Approach (for small $N$):**  
   * Exact execution of transition rules from one generation to the next.  
   * Provides exact answers to user queries.  
   * Uses state hashing to quickly detect whether the system has reached a stable state or entered a cycle.  
2. **Machine Learning Approach – NN / RL (for large $N$):**

   * **Data Collection:** The deterministic simulator is used to generate a dataset of instances (recording the evolution of the automaton over the first $k$ steps from various initial configurations).  
   * **Neural Networks (NN):** Training models on the initial simulated generations to approximate answers for distant iterations with minimal error (e.g., estimating the count of type $X$ cells at step $N$, predicting the final state, or classifying the automaton's behavior as stable, cyclic, or chaotic). The five questions will be coupled (if possible – such as Q1 & Q3) and for each group a NN will be trained.  
   * **Reinforcement Learning (RL):** Another approach we considered is using RL, a solution suited either for modeling automata that involve mobile entities or for efficiently searching for an initial configuration that leads to a specific target pattern on the grid.

### C. Natural Language Processing (NLP)

All processing will be performed strictly locally, without relying on external APIs. The input text will be translated into specific JSON text that represents the described automaton. The data will be validated both by the user and code.
