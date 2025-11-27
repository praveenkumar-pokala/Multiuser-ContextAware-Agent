# Multi‑User, Conversational Agentic AI with Tool Calling

Hands‑on notebooks that take you from **custom tools** to a full **multi‑user, context‑aware conversational agent** using LangChain, OpenAI, and real API endpoints.

> Tool calling is how LLMs evolve from talking to doing.  
> This repo focuses on that evolution, step by step.

---

## 🧠 What you will learn

By working through the notebooks in order, you will learn:

- Why LLMs need tools and how tools let models act beyond plain text.
- How to wrap real API endpoints as **custom tools** with clear input/output schemas.
- How to build a **research agent** with LangChain’s legacy `AgentExecutor` and tools.
- How to design a **multi‑user, context‑aware conversational agent** that persists memory in a database.
- How to reason about **who** is speaking (user id), **what** they did (tool calls), and **why** the agent responds in a specific way (traceable reasoning).

---

## 📂 Repo structure

```text
.
├── NB1_Custom_Tools_Calling_Understanding.ipynb
├── NB2_Langchain_Tool_calling_research_agent.ipynb
├── NB_3_Multiuser_ContextAware_Agent.ipynb
└── README.md  ← you are here
```

### 1️⃣ `NB1_Custom_Tools_Calling_Understanding.ipynb`

Foundation notebook.

- Intuition: *LLMs can think, but can they act?*
- Introduces why tool calling matters and how it changes the role of LLMs.
- Builds a **custom tool from a real API endpoint**:
  - Define the tool name, description, and argument schema.
  - Add validation and guardrails.
  - Call the tool from an LLM in a controlled loop.

Outcome: You understand the mental model of “LLM + tools” and can turn any HTTP API into an LLM‑callable tool.

---

### 2️⃣ `NB2_Langchain_Tool_calling_research_agent.ipynb`

From tools to **agents**.

- Uses LangChain’s legacy `AgentExecutor` to orchestrate:
  - LLM reasoning
  - Tool selection
  - Tool invocation
  - Final responses
- Shows how to:
  - Initialize agents with an LLM, prompt, and tool list.
  - Let the agent **decide which tool to call and with what arguments**.
  - Inspect intermediate steps (thought, action, observation) for debugging and teaching.
- Discusses why LangChain now recommends **LangGraph** for more complex agents, but this notebook is perfect to understand the classic agent loop.

Outcome: You can build a single‑user research agent that calls tools and explains how it arrived at its answer.

---

### 3️⃣ `NB_3_Multiuser_ContextAware_Agent.ipynb`

Scaling to **multi‑user, context‑aware conversations**.

- Builds a conversational agent that:
  - Serves multiple users.
  - Tracks each user’s session separately.
  - Stores conversation history and tool results in a SQL database.
- Focus areas:
  - Designing a **user/session model**.
  - Fetching the right context per user before each response.
  - Persisting agent messages and tool outputs for auditability and analytics.

Outcome: You can generalize from a single one‑off agent to a **production‑like multi‑user system** with memory and traceability.

---

## 🚀 Getting started

### 1. Clone the repo

```bash
git clone <your-repo-url>.git
cd <your-repo-folder>
```

### 2. Create and activate a virtual environment (recommended)

```bash
python -m venv .venv
source .venv/bin/activate   # macOS / Linux
# or
.venv\Scripts\activate    # Windows
```

### 3. Install dependencies

Create a `requirements.txt` similar to:

```text
langchain
langchain-community
langchain-openai
openai
python-dotenv
sqlalchemy
pydantic
ipykernel
jupyter
```

Then install:

```bash
pip install -r requirements.txt
```

### 4. Set your API keys

Most examples will require an OpenAI compatible API. Export the keys as environment variables, for example:

```bash
export OPENAI_API_KEY="your_api_key_here"
# or on Windows PowerShell:
# $env:OPENAI_API_KEY="your_api_key_here"
```

If some tools use external APIs (search, HTTP endpoints, etc.), set those keys too. The relevant cells in the notebooks will indicate what is needed.

### 5. Run the notebooks

```bash
jupyter notebook
```

Then open the notebooks in the following order:

1. `NB1_Custom_Tools_Calling_Understanding.ipynb`
2. `NB2_Langchain_Tool_calling_research_agent.ipynb`
3. `NB_3_Multiuser_ContextAware_Agent.ipynb`

---

## 🧩 Suggested learning path

While working through the notebooks, try to:

1. **Draw the loop**  
   For each notebook, sketch the cycle:  
   *User message → LLM reasoning → Tool selection → Tool call → Observation → Final answer*.

2. **Instrument the agent**  
   Print intermediate steps (thoughts, actions, tool inputs/outputs). It turns the notebook into an X‑ray of the agent.

3. **Extend the tools**  
   Replace the demo API with:
   - A domain API you care about (finance, travel, internal services).
   - A SQL query tool to talk to your own data.
   - A small retrieval tool on top of your documents.

4. **Think multi‑tenant early**  
   In the multi‑user notebook, imagine:
   - Ten users hitting the agent at once.
   - How you would partition data.
   - How you would debug a single user’s journey from logs.

---

## 📌 Ideas for extensions

- Add a **RAG tool** (retrieval‑augmented generation) so the agent can read your own docs.
- Swap the legacy `AgentExecutor` with **LangGraph** while keeping the same tools. Compare readability and control.
- Add **structured logging** (JSON logs) of every tool call and response.
- Wrap the multi‑user agent behind a **simple FastAPI / Flask API** to serve a front‑end.

---

## 🤝 How to use this repo in your own talks or workshops

- Use `NB1` as your “why tools matter” narrative.
- Use `NB2` to show the classic agent loop and demystify LangChain agents.
- Use `NB3` to talk about real‑world concerns: multi‑user context, memory, and observability.

You can adapt the notebooks to your domain and reuse them as a teaching pack for Agentic AI and tool calling.

---

If you build something interesting on top of these notebooks, consider adding:

- A short architecture diagram.
- A trace of one real user session.
- Notes on what broke in production and how you fixed it.

That is where the real learning happens. 🙂
