# 🧠 Multi-Step Reasoning Agent with Self-Checking

## 📖 Overview
This project implements a **Multi-Step Reasoning Agent** capable of solving structured word problems such as:

- ➕ Arithmetic (e.g., `2+3`)  
- ⏱ Time differences (e.g., train departure and arrival)  
- 🧩 General reasoning (e.g., “Alice has 3 red apples and twice as many green apples as red. How many apples does she have in total?”)  

The agent uses a combination of:

1. 🐍 **Python logic** for deterministic problems (arithmetic, time).  
2. 🤖 **Gemini LLM** for general reasoning tasks.  

It also performs **self-verification** ✅ to ensure correctness before returning the final answer.

The output JSON contains:

- `answer`: 📝 the user-facing final answer  
- `reasoning_visible_to_user`: 💡 a short explanation of reasoning  
- `metadata`: 🗂 internal logs including plan, verification, and retries (for debugging)

## How to Run

1. Install dependencies: !pip install google-generativeai
2. Set your API key
3. Run the agent
4. Question: What is 2+3?
5. View the answer
   - The agent outputs a JSON with:
   - `answer`: the user-facing final answer  
   - `reasoning_visible_to_user`: a short explanation of reasoning
  
## Where Prompts Live

All prompts are embedded inside the Python script:

1. PLANNER_PROMPT: generates a step-by-step plan
2. EXECUTOR_PROMPT: executes the plan (or uses Python for arithmetic/time)
3. VERIFIER_PROMPT: validates the solution

Prompts can be moved to separate .txt files if preferred.

## Assumptions

1. Arithmetic questions are simple expressions evaluated directly using Python.
2. Time difference questions are in HH:MM format.
3. LLM is used only for multi-step reasoning questions.
4. Users only see answer and reasoning_visible_to_user. Internal metadata is mainly for debugging.

## Prompt Documentation
### Planner
1. Breaks the question into numbered steps.
2. Extracts quantities, rules, and constraints without solving.

### Executor
1. Follows the plan exactly to produce a final answer.
2. Uses Python for simple questions; LLM for complex reasoning.

### Verifier
1. Validates the solution before presenting it to the user.
2. Python outputs are deterministic and auto-verified; LLM outputs are checked with another call.
