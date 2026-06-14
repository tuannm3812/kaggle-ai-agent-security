# EDA Insights

## 1. Run Evidence

Kaggle notebook:

- Kernel: `tuannm3812/ai-agent-security-01-eda`
- Successful version: `3`
- URL: <https://www.kaggle.com/code/tuannm3812/ai-agent-security-01-eda>
- Pulled outputs: `artifacts/runs/kaggle-01-eda-v3/`

The pulled artifacts are intentionally kept out of git. The most important
files are:

- `01_eda_summary.json`
- `01_pattern_census.csv`
- `01_candidate_surface_examples.csv`
- `01_tool_dictionary.csv`
- `ai-agent-security-01-eda.log`

## 2. Package Scale

The official Kaggle run found:

| Area | Count |
| --- | ---: |
| SDK Python files | 102 |
| Offline web pages | 19,679 |
| Inbox emails | 8,746 |
| Seed filesystem files | 24 |

The fixture corpus is large enough that a manual prompt list will plateau
quickly. We should generate prompt banks from fixture ids and pattern groups.

## 3. Fixture Shape

Top fixture families:

| Surface | Top prefix | Count |
| --- | --- | ---: |
| Web | `scale` | 11,527 |
| Email | `scale` | 7,711 |

The `scale` family dominates both surfaces, but `rt`, `long`, `new`, and `mh`
are more interesting for early attack development because they include clearer
red-team and multi-hop structure.

## 4. Attack-Surface Counts

Top matched patterns from the Kaggle EDA run:

| Source | Pattern | Count |
| --- | --- | ---: |
| Email | `shell.run_or_diagnostic` | 4,264 |
| Web | `shell.run_or_diagnostic` | 3,734 |
| Web | `http.post_or_upload` | 3,436 |
| Web | `explicit_multi_hop` | 3,393 |
| Email | `http.post_or_upload` | 2,154 |
| Web | `fs.delete_or_remove` | 1,959 |
| Web | `fs.write_or_append` | 1,919 |
| Web | `email.send_or_share` | 1,792 |
| Email | `fs.delete_or_remove` | 1,376 |
| Email | `email.send_or_share` | 1,263 |

Implication: web has the richest multi-hop and share/write/delete surface;
email has a strong diagnostic/exec surface. The first baseline should test both.

## 5. Strategy Implications

Priority for `02_baseline_attack.ipynb`:

1. Build a prompt bank from top web and email ids, not hand-written prompts only.
2. Start with high-confidence base ids: `page_2`, `page_4`, `page_10`,
   `email_1`, `email_7`, and a few `long`/`new` multi-hop ids.
3. Replay every returned candidate and store predicates plus
   `score_cell_signature.hash`.
4. Dedupe by score-cell hash before expanding prompt volume.
5. Keep prompt wording careful: avoid explicit authorization words when trying
   to trigger `UNTRUSTED_TO_ACTION` or `CONFUSED_DEPUTY`.

The next notebook should produce the first manifest, not chase leaderboard
submission yet.

