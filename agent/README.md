# LIFE Pathfinder local assistant

Status: **local-first operational baseline / human review required**

LIFE Pathfinder is the MyZubster environmental pilot and replication navigator. It runs locally with Ollama and indexes Markdown in this repository into a private SQLite FTS5 knowledge base.

## Workflow

`DISCOVER → QUALIFY → DESIGN PILOT → DEFINE EVIDENCE → REVIEW → REPLICATE`

## Safety boundary

Treat LIFE work as exploration unless official evidence proves otherwise; never claim EU/CINEA funding, approval, partnership, measured impact, or pilot completion without a cited source.

The assistant is advisory. It cannot approve work, declare external payments final, create institutional authority, or replace human/security review.

## Run

```bash
ollama pull qwen2.5:3b
python3 agent/assistant.py index
python3 agent/assistant.py health
python3 agent/assistant.py ask "Summarize the verified current state and cite sources"
```

Optional environment variables: `MYZUBSTER_MODEL`, `OLLAMA_URL`, and `MYZUBSTER_AGENT_DB`. The generated database stays under `.local/` by default and must not be committed.

## Test

```bash
python3 -m unittest agent/tests/test_assistant.py
```

## Knowledge rules

- Index only repository Markdown that is safe for local use.
- Files matching common private-key, wallet-seed, or token patterns are skipped.
- Keep facts distinct from narrative character lore.
- Refresh the index after documentation changes.
