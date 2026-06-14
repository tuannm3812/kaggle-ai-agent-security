# Agent Workflow

## 1. Working Style

Use short, scoped iterations:

1. Inspect official files and update notes.
2. Build the smallest valid baseline.
3. Validate replay and packaging.
4. Expand one attack family at a time.
5. Compare manifests before changing submission strategy.

## 2. Repo Boundaries

- `notebooks/` is the executable source of truth.
- `docs/` stores decisions, findings, score notes, and workflow updates.
- `scripts/` stores maintenance helpers only.
- `artifacts/` stores generated local files and remains gitignored.

## 3. Run Logging

Each serious run should record:

- date;
- notebook name;
- git commit or working-tree note;
- input data version;
- candidate count;
- local validation count;
- submission artifact path;
- result or reason for not submitting.

