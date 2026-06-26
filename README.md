# novamart-context — the team's communal analytics context

The shared, version-controlled context the AI analyst reads: the semantic layer and metric definitions
for the NovaMart dataset. This repo is the team's single source of truth.

- `datasets/novamart/semantic/` — entities, relationships, dimensions (synonyms + real sample values),
  measures, named filters, verified queries, custom instructions.
- `datasets/novamart/metrics/index.yaml` — meaning-only metric definitions (no SQL, no stored numbers).

How it is used: an analyst points at this repo via its `context-source.yaml`; `knowledge-bootstrap` pulls
it and loads the semantic layer before writing any SQL. Changes come in as **pull requests** and go through
review (proposed -> verified) before the team pulls them.

What is NOT here: the gold / answer-key. That stays hidden with the eval harness — if the agent could read
the answers it would cheat.
