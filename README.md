# 🧠 Multi-Agent Game Engine

This project defines and runs a simple text-based game engine using a state machine model, powered by the [LangGraph](https://github.com/langchain-ai/langgraph) library. It features two mini-games — a **Number Guessing Game** and a **Word Deduction Game** — using a dynamic graph-based system to control user interaction flow.

---

## 🔧 Core Components

### 1. `GameState` (TypedDict)
Represents the complete game state, including:

- `current_game`: Current game in play
- `number_guess_min`, `number_guess_max`: Range for number guessing
- `number_game_count`, `word_game_count`: Game counters
- `session_games`: List of games played in the session
- Clue attempts and word tracking fields for the word game

---

### 2. 🧠 Agents (Functions handling game logic)

#### a. `game_selector_agent`
- Prompts the user to choose a game:
  - Number Game
  - Word Game
  - Exit
- Sets the `_next` field to determine the next state

#### b. `number_game_agent`
- A binary search guessing game:
  - Asks if the number is greater than the midpoint
  - Narrows the range based on user response
  - Ends when `min = max` (correct guess)

#### c. `word_game_agent`
- Deduction game using yes/no clues:
  - Filters a list of possible words based on predefined clue logic
  - Guesses when only one candidate remains
  - Resets if the list is exhausted or guessing fails

---

### 3. `ExecutionTracker`
- Tracks visited nodes (states) during game execution
- Records game type and transition info
- Used for post-session visualization of the execution trace

---

### 4. 🔀 Routing
- `router()` reads the `_next` key in state to determine the next node
- Drives the state transition logic based on user choices

---

### 5. 🧭 Graph Definition (LangGraph)
- Uses `langgraph.StateGraph` to:
  - Define each node (state handler/agent)
  - Set the entry point
  - Establish conditional transitions between states using the router

---

## 🎨 Visualization Tools

### a. `visualize_structure()`
- Draws the static architecture of the game state machine
- Displays:
  - Game state nodes
  - Transitions (solid for new states, dashed for repeats)

### b. `visualize_execution()`
- Visualizes the actual execution path of a session
- Uses `ExecutionTracker` logs to render a directed graph of node transitions

---

## 🚀 Getting Started

1. Clone the repo
2. Install dependencies:
   ```bash
   pip install langgraph
