<div align="center">

# Mohammed Hamzah

### Building agentic systems that are **cheaper**, **friendlier**, and **lighter**.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Mohammed%20Hamzah-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/YOUR-LINKEDIN/)
[![Email](https://img.shields.io/badge/Email-your%40email.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:your@email.com)
[![Followers](https://img.shields.io/github/followers/ForestDweller014?style=for-the-badge&logo=github&logoColor=white&color=181717&label=Follow)](https://github.com/ForestDweller014)

</div>

---

## `> mission`

AI is getting more capable, but the default way we scale it — bigger models, bigger prompts, bigger GPU bills — doesn't hold up. The cost curve, the usability gap, and the energy footprint all point the same direction: **the next wave of agentic systems has to do more with less.**

I build toward that in three ways:

| | Principle | What it means in practice |
|---|---|---|
| 💸 | **Cheaper** | Route work to small, specialized models with tightly bounded context, instead of throwing one giant model and a giant prompt at every problem. |
| 🧭 | **Friendlier** | Every agent action should be inspectable — traces, graphs, and artifacts a human can actually read, audit, and replay. |
| 🌱 | **Lighter** | Fewer tokens, smaller models, controlled inference. Less compute per task is both an engineering win and a carbon win. |

Cornell '26 — Information Science + Applied Economics & Management. Currently building inference-side infrastructure for multi-agent systems and looking for **full-time AI/ML engineering roles** in inference and agent infrastructure.

```python
hamzah = {
    "education":  "Cornell University · Info Sci + AEM · Class of 2026",
    "focus":      ["agentic systems", "inference infrastructure", "interpretability"],
    "building":   ["multi-agent orchestration", "activation steering", "ML data pipelines"],
    "thesis":     "capable AI should get cheaper and lighter, not just bigger",
    "open_to":    "full-time AI/ML engineering roles",
}
```

---

## `> the_system`

My core projects aren't isolated demos — they form one pipeline. **Dullahan** runs swarms of small expert agents over a knowledge graph. Every run leaves behind a machine-readable action graph. **Specter** consumes that graph, puts each expert's answer on trial, and corrects the model *at the activation level* rather than by stuffing more text into the prompt. **Fintan** is the data discipline underneath: turning noisy real-world market data into clean, labeled training signal.

```mermaid
flowchart LR
    A["📚 Knowledge<br/>(docs, code, data)"] --> B["🐎 Dullahan<br/>expert swarm over a<br/>clustered context graph"]
    B --> C["📊 Action graph trace<br/>(every query, context,<br/>and answer — auditable)"]
    C --> D["👻 Specter<br/>debate-based validation +<br/>activation-level steering"]
    D -->|"steered inference"| B
    E["📈 Fintan<br/>labeled training data<br/>from live market feeds"] -.->|"real-world data discipline"| A
```

**Why this matters right now:** the industry is converging on exactly these problems — multi-agent orchestration, context engineering, small-model routing, and controllability beyond prompting. This stack is my attempt to build all four from first principles.

---

## `> featured_projects`

### 🐎 [Dullahan](https://github.com/ForestDweller014/Dullahan) — hierarchical agent swarm with reliable context control

**Plain English:** instead of asking one huge model one huge question, Dullahan breaks a task into small questions, hands each one to a small specialist agent that only sees the context it needs, and records every step so you can audit exactly what happened.

**Under the hood:** knowledge lives in a K-partitioned graph; a **Context Augmentation Layer (CAL)** builds token-budgeted context bundles per subquery from graph-backed retrieval (local vector index or PostgreSQL + pgvector); an **Expert Dispatch Layer (EDL)** routes each subquery to a cluster-specialized SLM via embedding attention. Experts recurse under hard depth/breadth/instance limits. Every run exports YAML/Markdown artifacts plus a JSON + Mermaid action graph.

**Why it's cheaper and lighter:** each step is a small model with a focused context slice — not a frontier model rereading the whole world. Context bundles record their own token-reduction stats per subquery.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/pgvector-316192?style=flat-square&logo=postgresql&logoColor=white)
![MCP](https://img.shields.io/badge/MCP-tools-181717?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white)

---

### 👻 [Specter](https://github.com/ForestDweller014/Specter) — courtroom validation + activation-level steering for expert SLMs

**Plain English:** Specter checks an AI agent's work by staging a structured debate — prosecutor, defense, judge — over every answer it gave. Then, instead of just telling the model "do better" in text, it finds *where inside the network* the feedback matters and corrects the model there directly.

**Under the hood:** consumes Dullahan-style action graphs, runs multi-round debate over each answered node and delegation edge, then uses **TransformerLens** to localize debate feedback to specific residual-stream layer/token positions via contrast pairs. It derives steering vectors, materializes reversible activation hooks (`scaled_vector = direction × prosecution_strength × feedback_scale`), and reruns expert inference with the vectors injected — steering the computation instead of diluting the prompt.

**Why it matters:** prompt-based feedback competes with everything else in context. Activation steering is targeted, measurable, and doesn't grow the token bill. This is interpretability put to work as infrastructure.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TransformerLens](https://img.shields.io/badge/TransformerLens-7A3EF2?style=flat-square)
![Interpretability](https://img.shields.io/badge/Activation%20Steering-D97706?style=flat-square&logo=anthropic&logoColor=white)
![LLM Agents](https://img.shields.io/badge/LLM%20Agents-412991?style=flat-square&logo=openai&logoColor=white)

---

### 📈 [Fintan](https://github.com/ForestDweller014/Fintan) — labeled ML training data from live US equity markets

**Plain English:** models are only as good as their data. Fintan turns raw, messy, minute-by-minute stock market data into clean, consistent training examples: "here's what the market looked like, and here's what the optimal trade decision would have been."

**Under the hood:** async, rate-limited fetching of 1-minute OHLCV bars for ~200 US equities from Alpaca, respecting NYSE calendars. Computes six scale-invariant features — RSI (Wilder smoothing), MACD histogram z-score, ATR, OBV, Bollinger %B/bandwidth via **Welford's online variance algorithm**, and Fibonacci range position. Labels each signal point by forward lookahead: optimal bracket and trailing-stop exit ratios, emitted as `{inputs, labels}` JSONL. Full CLI covers fetch, feature, label, and brokerage workflows.

**Why it matters:** numerically stable streaming statistics, honest labeling, and pipeline discipline — the unglamorous 80% of ML that determines whether the model on top is real.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![aiohttp](https://img.shields.io/badge/aiohttp-2C5BB4?style=flat-square&logo=aiohttp&logoColor=white)
![Alpaca](https://img.shields.io/badge/Alpaca%20API-FFD700?style=flat-square&logoColor=black)
![Quant](https://img.shields.io/badge/Quant%20Features-150458?style=flat-square&logo=pandas&logoColor=white)

---

## `> tech_stack`

**Languages**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-336791?style=flat-square&logo=postgresql&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

**AI / ML**
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![TransformerLens](https://img.shields.io/badge/TransformerLens-7A3EF2?style=flat-square)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black)
![vLLM](https://img.shields.io/badge/vLLM-30A46C?style=flat-square)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)

**Agent & Inference Infrastructure**
![MCP](https://img.shields.io/badge/MCP-181717?style=flat-square)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![pgvector](https://img.shields.io/badge/pgvector-316192?style=flat-square&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)

**Tooling**
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white)

---

## `> currently`

```
[ ▰▰▰▰▰▰▱ ]  Dullahan + Specter integration      ·  validation-steered expert swarms
[ ▰▰▰▰▰▱▱ ]  Inference optimization              ·  small-model serving, context budgets
[ ▰▰▰▰▱▱▱ ]  Interpretability research           ·  activation steering as infrastructure
[ ▰▰▰▰▰▰▰ ]  Full-time AI/ML engineering search  ·  inference & agent infrastructure roles
```

---

<div align="center">

![GitHub stats](https://github-readme-stats.vercel.app/api?username=ForestDweller014&show_icons=true&theme=graywhite&hide_border=true&include_all_commits=true&hide=stars)

*Cheaper. Friendlier. Lighter. Get to work.*

</div>