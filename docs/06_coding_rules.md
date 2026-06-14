# Coding Rules

## 1. Repository Scope

This repository is notebook-first. Kaggle notebooks are the executable source of
truth, while `docs/` captures analysis, run notes, and decisions.

Keep the root small:

- `notebooks/` for Kaggle notebooks.
- `docs/` for reports, results, and supporting artifacts.
- `scripts/` for maintenance helpers.
- `artifacts/` for generated local files, kept out of git.

## 2. Notebook Style

Each notebook should include:

- a short purpose statement at the top;
- a configuration section near the top;
- Kaggle and local path auto-detection where practical;
- concise markdown notes after important results;
- explicit artifact-writing cells for manifests, traces, and submissions.

Keep final submission notebooks deterministic and avoid internet access during
Kaggle reruns.

## 3. Python Style

- Follow PEP 8.
- Use 4 spaces for indentation.
- Prefer small functions with clear names.
- Add type hints for reusable utilities.
- Use comments to explain why, not what.
- Keep generated files out of git.

## 4. Artifact Naming

Use stable, numbered names:

- `notebooks/01_eda.ipynb`
- `notebooks/02_baseline_attack.ipynb`
- `notebooks/03_replay_validation.ipynb`
- `notebooks/04_submission_packaging.ipynb`
- `docs/01_instructions.md`
- `docs/02_competition_notes.md`
- `docs/03_attack_workflow.md`
- `docs/04_agent_workflow.md`
- `docs/06_coding_rules.md`

## 5. Git Hygiene

Do not commit:

- raw Kaggle competition data;
- generated submissions;
- replay logs;
- large cached arrays or tables;
- virtual environments;
- notebook checkpoints;
- Kaggle credentials.

Use `python scripts/clean_notebook_outputs.py` before committing notebooks with
changed executable logic.

