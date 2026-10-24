# LLM Agents Study Session — Full-Day Program

**Group size:** ~6 people · **Format:** all-day (opening talk → afternoon hands-on → dinner together)
**Status:** draft for team review — please leave your comments on this pull request before the session.

---

## 1. Opening Talk — Foundations: Quoting "Attention Is All You Need"

We open the day by quoting the Transformer paper directly, so the intro slide is accurate.
All facts below are taken from the paper itself — Vaswani et al., *"Attention Is All You Need"* (arXiv:1706.03762) — and were checked against the paper's own text (abstract, Section 3 "Model Architecture", and Section 5 "Results").

### Quotation for the intro slide

> "The Transformer follows this overall architecture using stacked self-attention and point-wise, fully connected layers for both the encoder and decoder, shown in the left and right halves of Figure 1, respectively."

This is the paper's own one-sentence description of the Transformer architecture (Section 3, *Model Architecture*).

### Headline WMT 2014 results (newstest2014 test sets)

| Task | BLEU | Notes |
|---|---|---|
| English→German | **28.4** | New state of the art — outperforms the best previously reported models (including ensembles) by more than 2.0 BLEU |
| English→French | **41.8** | New single-model state of the art |

For reference, the Transformer **base** model scores 27.3 (EN→DE) and 38.1 (EN→FR).

### Training cost

- The big model was trained for **3.5 days on 8 P100 GPUs** (the paper's abstract likewise describes training for 3.5 days on eight GPUs).
- Estimated training compute: **2.3 × 10¹⁹ FLOPs** for the big model, and 3.3 × 10¹⁸ FLOPs for the base model — "a small fraction of the training costs of the best models from the literature."

### Base model dimensions (intro slide)

- **Hidden dimension (d_model): 512**
- **Attention heads: 8**
- Context for the slide: N = 6 encoder and 6 decoder layers, feed-forward dimension d_ff = 2048, ~65M parameters.

---

## 2. Afternoon Hands-On — Model Context Protocol (MCP)

### The session video (reprise for the group)

**"MCP In 26 Minutes (Model Context Protocol)"** — by **Tina Huang** (YouTube channel @TinaHuang1)
▶ https://www.youtube.com/watch?v=kOhLoixrJXo (published 2025-10-15, ~26 minutes)

A beginner-friendly overview of MCP fundamentals — architecture (clients, servers, tools, resources, prompts), how MCP servers work, and how to build and use MCP integrations.

### Follow-up videos from Tina Huang's channel — watch in this order

1. **Building AI Agents In 44 Minutes** — the six-component agent architecture (model, tools, knowledge/memory, speech, guardrails, orchestration) with her first introduction to MCP; watch this first to see exactly where MCP fits inside an agent stack.
2. **8 Hour AI Agents Course in 30 Minutes** — a condensed tour of the whole agents landscape, released shortly after the MCP video; good consolidation of everything the primer introduces, including multi-agent patterns.
3. **Context Engineering Clearly Explained** — moves one layer up from MCP: controlling what your agent actually sees; the natural companion to tool connectivity once servers are wired up.
4. **Local AI Agents In 26 Minutes** — running agents and MCP servers locally with open-source models; practical for lab machines and privacy-sensitive data.

### Suggested hands-on flow (afternoon)

1. Rewatch "MCP In 26 Minutes" together (or assign as pre-watching) and collect questions.
2. Walk through the host → client → server architecture and the three primitives (tools, resources, prompts) — `research-notes.md` in this repo is the reference.
3. Hands-on: connect an MCP client to a public server, then build a minimal server of our own and call its tool from the host.
4. Close with a short discussion of where each of us could use MCP in current lab projects.

---

## 3. Dinner — Cooking for Six (Two Colleagues Are Vegetarian)

Menu drawn from our Chinese home-cooking recipe collection: two vegetarian dishes (素菜), one soup (汤), one meat dish (荤菜).

| Course | Dish | Main ingredients |
|---|---|---|
| 素菜 | **地三鲜** (sautéed potato, eggplant & pepper) | eggplant (茄子), potato (土豆), green peppers (尖椒), with scallion, ginger, garlic, doubanjiang, soy sauce and a cornstarch slurry |
| 素菜 | **松仁玉米** (pine-nut sweet corn) | sweet corn kernels, toasted pine nuts, carrot (for colour), sugar, salt, cornstarch |
| 汤 | **紫菜蛋花汤** (seaweed & egg-drop soup) | dried seaweed (紫菜), eggs, scallions, salt and oil — shrimp is optional in the recipe, so leave it out and the soup stays vegetarian |
| 荤菜 | **宫保鸡丁** (Kung Pao chicken) | chicken thigh (or breast), scallion, dried chillies, roasted peanuts, light soy sauce, vinegar, sugar, Shaoxing wine, Sichuan peppercorn, cornstarch |

Notes:

- Both vegetarian dishes are fully meat-free, and the soup is vegetarian as long as the optional shrimp is skipped — the two vegetarian colleagues get three of the four courses.
- Recipe quantities in the collection are written per serving: multiply by six when shopping.
- 宫保鸡丁 is rated the hardest of the four (★★★★ in the collection); it needs the chicken marinated about an hour ahead, so start it before the afternoon session wraps up.

---

## Reviewing This Plan

This document is open for comments as a pull request. Please review and comment before the session — especially the watch order in Section 2 and the menu in Section 3 (allergies/aversion to any ingredient).
