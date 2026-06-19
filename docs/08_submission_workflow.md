# Submission Workflow

## 1. What Gets Submitted

This is a notebook-only competition. The notebook is the submission source; a
locally prepared `submission.csv` is not the input artifact.

The notebook must:

1. generate `/kaggle/working/attack.py`;
2. define `AttackAlgorithm` in that file;
3. start `JEDAttackInferenceServer` when `KAGGLE_IS_COMPETITION_RERUN` is set.

The competition gateway loads the served attack, evaluates its returned
`AttackCandidate` chains, and writes `submission.csv` automatically.

## 2. Execution States

| State | Trigger | Expected outputs | Leaderboard result |
| --- | --- | --- | --- |
| Local execution | Run notebook locally | Local `attack.py`, manifest, summary | None |
| Normal Kaggle version | Save/run a notebook version | `/kaggle/working/attack.py`, manifest, summary, log | None |
| Competition rerun | Submit a completed notebook version | Gateway-generated `submission.csv` and `submission_details.json` | Yes |

A normal Kaggle version displaying `competition_rerun: False` is healthy but
not submitted. It should not be expected to contain `submission.csv`.

## 3. Generated CSV Schema

The official gateway writes:

```csv
Id,Score
gpt_oss_public,<score>
gemma_public,<score>
```

Private guardrail rows may also appear when enabled by the evaluator. These
scores are computed during the trusted competition rerun; fabricating this file
locally would not evaluate the attack and would not be a valid substitute.

## 4. Release Checklist

Before saving a Kaggle version:

1. Execute the notebook locally and confirm its embedded outputs match the
   source version and candidate count.
2. Confirm `attack.py` is under 5 MB and defines the required class.
3. Confirm every candidate has 1-32 messages and every message is at most 2,000
   characters.
4. Synchronize the executed notebook into its `kaggle/` kernel directory.
5. Push the kernel and wait for `KernelWorkerStatus.COMPLETE`.
6. Pull the normal-run artifacts and verify version, candidate count, and
   families.

To submit:

1. Open the completed Kaggle notebook version.
2. Choose **Submit to Competition** for that exact version.
3. Wait for the competition rerun and submission status to complete.
4. Check the score with the Kaggle submissions page or CLI.
5. Record the kernel version, submission reference, score, and artifact paths
   in the repository docs.

## 5. Current Release

- Kernel: `tuannm3812/ai-agent-security-02-baseline-attack`
- Kaggle kernel version: `7`
- Strategy version inside notebook: `v6`
- Verified normal-run candidate count: `50`
- Verified families: `25` exfiltration and `25` confused deputy
- Competition submission: pending manual submission of Kaggle Version 7

Earlier submitted Kaggle Versions 3, 5, and 6 all contained the stale v3
20-candidate attack and scored `0.000`. Version 7 is the first verified Kaggle
run containing the actual v6 strategy.
