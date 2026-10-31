# Simple Reflex Vacuum Cleaner Agent

A small Python notebook that implements the classic **two-square vacuum world** from Artificial Intelligence. A **simple reflex agent** moves between two locations and cleans any dirt it finds, deciding only from what it currently perceives.

- **Course:** Artificial Intelligence
- **Author:** Maira (ID 41362)
- **Notebook:** `notebookc8d0247126.ipynb` (Kaggle, Python 3, no internet or GPU needed)

---

## Overview

The world has two locations, **A** and **B**. Each one is either clean (`0`) or dirty (`1`). The agent starts in one of them and, at every step, perceives its location and whether that square is dirty. It then picks one action.

| Concept | In this project |
|---|---|
| **Environment** | Two squares, `A` and `B`, each clean or dirty |
| **Percept** | `(location, dirty)`, for example `('B', 1)` |
| **Actions** | `Suck`, `Left`, `Right` |
| **Agent type** | Simple reflex agent (condition-action rules, no memory) |
| **Performance measure** | +10 for each `Suck`, -1 for each move |

---

## How It Works

### 1. `VacuumEnvironment`
Models the world.

- `status`: dictionary with the state of each square, e.g. `{'A': 1, 'B': 0}`
- `agent_location`: where the agent currently is
- `percept()`: returns `(location, dirty)` for the agent's current square
- `execute(action)`: applies the action
  - `Suck` cleans the current square
  - `Right` moves the agent to `B`
  - `Left` moves the agent to `A`

By default, the environment starts with random dirt and a random agent position.

### 2. `reflex_vacuum_agent(percept)`
The agent's decision rules, based only on the current percept:

```
IF the current square is dirty  -> Suck
ELSE IF location is A           -> Right
ELSE                            -> Left
```

### 3. Simulation loop
The demo sets a fixed starting state (both squares dirty, agent at `B`), then runs 4 steps. At each step it:

1. Reads the percept
2. Chooses an action with the agent function
3. Executes the action in the environment
4. Updates the score (+10 for cleaning, -1 for moving) and prints the result

---

## Example Output

```
Initial state : {'A': 1, 'B': 1} | Agent at B
Step 1: percept=('B', 1) -> action=Suck  | world={'A': 1, 'B': 0}
Step 2: percept=('B', 0) -> action=Left  | world={'A': 1, 'B': 0}
Step 3: percept=('A', 1) -> action=Suck  | world={'A': 0, 'B': 0}
Step 4: percept=('A', 0) -> action=Right | world={'A': 0, 'B': 0}
Final state   : {'A': 0, 'B': 0}
Performance score: 18
```

**Score breakdown:** 10 (Suck) - 1 (Left) + 10 (Suck) - 1 (Right) = **18**

Both squares are clean by step 3. In step 4 the agent keeps moving because a simple reflex agent has no memory and no way to know the whole world is clean.

---

## How to Run

1. Open `notebookc8d0247126.ipynb` in Kaggle, Google Colab, or Jupyter.
2. Run the single code cell.

Or run it locally:

```bash
pip install notebook
jupyter notebook notebookc8d0247126.ipynb
```

Only Python's built-in `random` module is used, so there are no extra dependencies.

---

## Key Concepts Demonstrated

- Agent, environment, percept, and action
- Simple reflex agents and condition-action rules
- Performance measures and rational behavior
- Partially observable environments (the agent only sees its own square)

---

## Possible Extensions

- Stop the agent once both squares are clean (add a model or memory, making it a **model-based reflex agent**)
- Expand the world to more squares or a grid
- Make the `Suck` action fail sometimes (a stochastic environment)
- Compare against a random agent over many runs and average the scores
- Add a penalty for energy used or a time limit

---

## Files

| File | Description |
|---|---|
| `notebookc8d0247126.ipynb` | Notebook with the environment, agent, and simulation |
| `README.md` | This document |
