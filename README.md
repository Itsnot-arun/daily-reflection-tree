# Daily Reflection Tree
**DT Fellowship Assignment | Arun K**

---

## What's in this repo

```
/tree/
  reflection-tree.json       ← Part A: the full decision tree (35 nodes)

/agent/
  index.html                 ← Part B: runnable web agent (open in browser, no server needed)

write-up.md                  ← Design rationale (max 2 pages)
README.md                    ← This file
```

---

## How to read the tree

The tree is a flat JSON array of nodes. Each node has:

| Field | Purpose |
|---|---|
| `id` | Unique node identifier |
| `parentId` | Which node this is a child of |
| `type` | `start`, `question`, `decision`, `reflection`, `bridge`, `summary`, `end` |
| `text` | What the employee sees. `{NODE.answer}` is replaced with prior answers |
| `options` | For `question`: array of fixed choices. For `decision`: routing rules |
| `target` | Next node to jump to (bridges, reflections, summary) |
| `signal` | What this node records in state (`axis1:internal`, `axis2:contribution`, etc.) |

### Decision node routing

Decision nodes use pipe-separated routing rules:

```
answer=Productive|Mixed:A1_Q_HIGH;answer=Tough|Frustrating:A1_Q_LOW
```

This reads: "If previous answer was Productive or Mixed → go to A1_Q_HIGH. If Tough or Frustrating → A1_Q_LOW."

Signal-based routing:

```
signal=axis1:internal:A1_R_INT;signal=axis1:external:A1_R_EXT
```

This reads: "If axis1 state is internal → go to A1_R_INT."

### State accumulation

As the employee answers questions, two things are tracked:
- `answers[nodeId]` — the selected option for each question node
- `signals[axis]` — the dominant signal per axis (first signal recorded wins)

At the summary node, the combination of all three axis signals selects one of 8 pre-written summary reflections. No text generation. No LLM call.

---

## How to run the agent

Just open `agent/index.html` in any browser. No server, no dependencies, no API key.

The agent:
- Loads the tree logic from embedded JS
- Walks nodes deterministically
- Auto-advances through `decision`, `bridge`, `reflection` nodes
- Waits for user input at `question` nodes
- Produces a 3-axis summary at the end

---

## The three axes

| Axis | Spectrum | Psychology |
|---|---|---|
| Locus | Victim ↔ Victor | Rotter (1954) Locus of Control; Dweck (2006) Growth Mindset |
| Orientation | Entitlement ↔ Contribution | Campbell et al. (2004) Psychological Entitlement; Organ (1988) OCB |
| Radius | Self-centric ↔ Altrocentric | Maslow (1969) Self-transcendence; Batson (2011) Perspective-taking |

---

## Contact

Arun K | arun9447835587@gmail.com | linkedin.com/in/arun-k-5449a6367
