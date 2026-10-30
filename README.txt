================================================================================
AI ASSIGNMENT: GENERAL-PURPOSE CLASSICAL REASONING SYSTEM
================================================================================

1. DIRECTORY STRUCTURE
----------------------
submission/
|-- reasoning_agent.ipynb   Complete self-contained implementation, evaluation,
|                           reasoning traces, and submission.csv generator
|-- report.pdf              Technical report describing representation, classical
|                           reasoning algorithms, experiments, and traces
|-- submission.csv          Generated predictions (id, label) across public test
|                           benchmarks (1,828 held-out queries)
`-- README.txt              Setup and execution instructions

2. REQUIREMENTS & ENVIRONMENT
-----------------------------
- Python 3.9+ (tested on Python 3.11.2)
- Zero external third-party packages are required for the core reasoning engine!
  All parsers, unification routines, Forward Chaining, Backward Chaining (DFS,
  BFS, UCS, A* search), First-Order Skolemization / Tseitin CNF / DPLL Resolution,
  and Structural Causal Abduction-Action-Prediction algorithms are implemented
  purely in standard Python (`re`, `json`, `csv`, `heapq`, `collections`, `difflib`).

3. HOW TO RUN
-------------
Option A: Run the Jupyter Notebook interactively or headlessly:
    jupyter nbconvert --to notebook --execute --inplace reasoning_agent.ipynb

Option B: Generate predictions on a custom/private test dataset (`private_test.jsonl`):
  Inside `reasoning_agent.ipynb`, call:
    generate_submission_csv("path/to/private_test.jsonl", "submission.csv")

  Or for a single natural-language (context, statement) query:
    agent = ClassicalReasoningAgent(search_strategy="astar")
    flag, trace = agent.predict(context, statement, return_trace=True)
    print("Predicted Flag:", flag)

4. SUMMARY OF PUBLIC BENCHMARK PERFORMANCE
------------------------------------------
- RuleTaker Train (n=1,000)      : 98.30% Accuracy | 0.074s total (0.074 ms/query)
- RuleTaker ID Test (n=250)      : 97.60% Accuracy | 0.018s total (0.072 ms/query)
- RuleTaker OOD Test (n=375)     : 99.47% Accuracy | 0.025s total (0.068 ms/query)
- CounterBench Alpha (n=1,000)   : 96.00% Accuracy | 0.050s total (0.050 ms/query)
- FOLIO Validation (n=203)       : 83.25% Binary Entailment (70.94% 3-Way) | 5.74s
- FOLIO Train (n=1,001)          : 83.42% Binary Entailment (71.73% 3-Way) | 37.05s
--------------------------------------------------------------------------------
- Held-Out Evaluation Total (n=1,828): 95.51% Accuracy (1,746/1,828) in 5.83s
- All Public Queries Total  (n=3,829): 93.08% Accuracy (3,564/3,829) in 42.95s
================================================================================
