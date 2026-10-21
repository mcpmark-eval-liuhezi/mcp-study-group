# Session 1 — Introduction to the Model Context Protocol

**Goal:** a beginner-friendly first session on how AI applications talk to external systems, grounded in the official MCP documentation.

**Pre-reading:** [`research-notes.md`](./research-notes.md) (on `main`) — the groundwork for the whole session. Read it before we meet; we will work through its sections together.

**Format:** 90 minutes, discussion-heavy, café setting. Bring a laptop.

## Agenda (90 minutes)

| # | Time | Duration | Topic | What happens |
|---|------|----------|-------|--------------|
| 1 | 0:00–0:10 | 10 min | Welcome & round of intros | Everyone says what they want to get out of the group. Quick recap of the notes file's structure so people know where to look. |
| 2 | 0:10–0:25 | 15 min | **What is MCP?** | Walk through the "What is MCP" section of `research-notes.md`: open standard, the USB-C analogy, who's behind it, and why it exists (fragmented one-off integrations → one protocol). |
| 3 | 0:25–0:45 | 20 min | **Architecture: hosts, clients, servers** | The client–server model: host = AI application, client = per-server connection, server = program providing context (local vs. remote). Sketch it on paper/whiteboard. |
| 4 | 0:45–1:05 | 20 min | **Tools, resources, prompts + transports** | The three primitives servers expose, with the database example (query tools, schema resource, analysis prompts). Then transports: stdio vs. Streamable HTTP — local subprocess vs. remote HTTP POST + SSE. |
| 5 | 1:05–1:20 | 15 min | **Use cases & where we go next** | Pick a use case from the notes (assistant + calendar/Notion, Figma→web app, enterprise data chatbots, Blender/3D printing) and discuss how our own work tools could be exposed as MCP servers. Agree session 2 topic. |
| 6 | 1:20–1:30 | 10 min | Wrap-up | Assign follow-ups via the "Prepare session 1 materials" issue; pick the café for next time if needed. |

## Venue shortlist (Beijing cafés)

Pick one at kickoff. All are well-rated and open every day; details current as of the search date — call ahead for a group table.

1. **Alba Cafe** — 70 Gulou E Ave, Dongcheng, Beijing 100009 (near Gulou). Daily 07:30–22:30. Well-rated (≈4.5), relaxed, roomy enough for a small group.
2. **Cafe Zarah** — 42 Gulou E Ave, Dongcheng, Beijing 100009. Daily 08:30–19:00. Well-rated (≈4.2), popular with the Gulou study/work crowd.
3. **Soloist Coffee Co.** — Yangmeizhuxie St, Xicheng District, Beijing 100031 (Dashilar hutongs). Daily 09:00–22:30. Well-rated (≈4.2), specialty coffee, good for afternoons/evenings.

## Materials

- `research-notes.md` — the notes file (pre-reading; also the reference doc for sections 2–5).
- This plan — timeboxes above; the discussion lead for each block should keep an eye on the clock.
- Follow-up checklist lives in the issue **"Prepare session 1 materials"**.
