# AI Agent Security - Multi-Step Tool Attacks

<p>
  <img alt="Kaggle" src="https://img.shields.io/badge/Kaggle-AI_Agent_Security-20BEFF?style=flat-square&logo=kaggle&logoColor=white">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&logo=python&logoColor=white">
  <img alt="Workflow" src="https://img.shields.io/badge/workflow-notebook--first-2E7D32?style=flat-square">
</p>

This repository is for the Kaggle competition
[AI Agent Security - Multi-Step Tool Attacks](https://www.kaggle.com/competitions/ai-agent-security-multi-step-tool-attacks).
The goal is to develop attack algorithms that identify reproducible multi-step
failures in tool-using AI agents.

The project is intentionally notebook-first, matching the structure used in the
other Kaggle repositories in this workspace. Notebooks hold executable
experiments, `docs/` captures reasoning and run notes, and `artifacts/` keeps
local generated files out of git.

## 1. Project Overview

This competition is closer to benchmark construction and adversarial workflow
search than standard tabular modeling. The core work is to understand the local
evaluator, generate replayable candidate attacks, validate that failures are
deterministic, and package outputs in the competition format.

Initial project goals:

- Reproduce the official local evaluation flow.
- Map the task, tool, policy, and failure surfaces.
- Build a baseline attack-generation notebook.
- Track every candidate with manifests and replay evidence.
- Keep final submission paths deterministic and Kaggle-compatible.

## 2. Repository Map

```text
.
|-- .gitignore
|-- README.md
|-- requirements.txt
|-- docs/
|   |-- 01_instructions.md
|   |-- 02_competition_notes.md
|   |-- 03_attack_workflow.md
|   |-- 04_agent_workflow.md
|   |-- 05_strategy.md
|   |-- 06_coding_rules.md
|   |-- 07_eda_insights.md
|   |-- 08_submission_workflow.md
|   `-- 09_reference_notebook_review.md
|-- notebooks/
|   |-- 01_eda.ipynb
|   |-- 02_baseline_attack.ipynb
|   |-- 03_replay_validation.ipynb
|   `-- 04_submission_packaging.ipynb
|-- scripts/
|   `-- clean_notebook_outputs.py
`-- artifacts/          # gitignored local outputs
    |-- analysis/
    |-- data/
    |-- runs/
    `-- submissions/
```

## 3. Setup

Create and activate a local environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Configure Kaggle credentials, then download competition files after accepting
the rules on Kaggle:

```powershell
kaggle competitions download -c ai-agent-security-multi-step-tool-attacks -p artifacts/data
```

If the Kaggle CLI is unavailable, install it from `requirements.txt` first and
retry inside the activated environment.

## 4. Notebook Workflow

| Notebook | Purpose |
| --- | --- |
| `01_eda.ipynb` | Inspect downloaded files, schemas, evaluator entry points, and sample outputs. |
| `02_baseline_attack.ipynb` | Build the first valid attack-generation baseline. |
| `03_replay_validation.ipynb` | Validate determinism, replay traces, and evaluator acceptance. |
| `04_submission_packaging.ipynb` | Audit release metadata and submission readiness. |

The normal Kaggle run must expose a file named `submission.csv` before the
version can be selected for submission. This repository writes a zero-valued
placeholder during normal runs. During the private competition rerun, the
notebook serves `/kaggle/working/attack.py` and the trusted gateway replaces the
placeholder role with real evaluated scores. See `docs/08_submission_workflow.md`.

## 5. Current Status

Kaggle kernel Version 7 is the first verified normal run of strategy v6. It
contains 50 candidates split between exfiltration and confused-deputy families.
Kaggle kernel Version 9 is the submission-ready normal run of strategy v7:
520 unique, direct, one-hop exfiltration candidates with 77-99 character prompts.
It exposes the required placeholder `submission.csv`; the next manual step is to
submit Version 9 to the competition. See `docs/09_reference_notebook_review.md`.
