# novamart-context — the team's communal analytics context

The shared, version-controlled context the AI analyst reads: the semantic layer and metric definitions
for the NovaMart dataset. This repo is the team's single source of truth.

- `datasets/novamart/semantic/` — entities, relationships, dimensions (synonyms + real sample values),
  measures, named filters. The semantic layer only.
- `datasets/novamart/metrics/index.yaml` — meaning-only metric definitions (no SQL, no stored numbers).
- `datasets/novamart/verified_queries.yaml` — verified question + known-good SQL examples.
- `datasets/novamart/custom_instructions.md` — the store's own small instructions file.

## The homes in this repo (the communal store)

Of the 10 places meaning can live in an agentic analyst, five are store-resident and each has a
labeled home here (a `# HOME:` line sits at the top of every file). The other homes are
analyst-side local or runtime and are NOT files in this repo.

| Home | Lives at |
|---|---|
| Meaning contracts (Home 3) | `datasets/novamart/metrics/index.yaml` |
| Semantic layer (Home 4) | `datasets/novamart/semantic/{entities,relationships,dimensions,measures,filters}.yaml` |
| Verified examples (Home 5) | `datasets/novamart/verified_queries.yaml` |
| Corrections (Home 6) | `datasets/novamart/corrections.md` |
| Store instructions | `datasets/novamart/custom_instructions.md` |

Not here (by design): resident instructions (Home 1), skills (Home 2), memory (Home 7) and the
schema/catalog home (Home 9) are **analyst-side local** (each analyst's own `.knowledge`); retrieval
(Home 8) and isolation/topology (Home 10) are **runtime** behaviors, not files. `schema_snapshots.yaml`
is only the semantic layer's freshness guard, not the schema home itself.

How it is used: an analyst points at this repo via its `context-source.yaml`; `knowledge-bootstrap` pulls
it and loads the semantic layer before writing any SQL. Changes come in as **pull requests** and go through
review (proposed -> verified) before the team pulls them.

What is NOT here: the gold / answer-key. That stays hidden with the eval harness — if the agent could read
the answers it would cheat.
