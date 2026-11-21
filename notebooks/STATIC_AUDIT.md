# DNABERT-2 Promoter Notebook Static Audit — 21 November 2026

## Scope
Inspected the three extracted promoter notebooks against their source cells. This is **static inspection**, not a fresh Colab execution, training reproduction, or independent DP guarantee verification.

## Confirmed issue and correction
**All three notebooks:** The compatibility-alias cell built `train_loader` using `collate_fn=collator`, but the data preparation cell defines `promoter_collator`, not `collator`. This would cause `NameError` in a fresh runtime. The audited notebooks replace it with `collate_fn=promoter_collator`.

## What is structurally present
- BiTFiT: setup, dataset reconstruction, model, baseline training.
- DP-SGD: setup, per-example gradient checks, privacy calibration, and separate epsilon 8/4/2 training cells.
- DP-SAT: setup, update-rule check, privacy audit, sampling code, and epsilon 4/2/8 training cells.
- Python parsing of every ordinary code cell succeeds. Colab magic and third-party runtime behavior were not executed.

## Remaining validation before submission
1. Run setup, dataset preparation, and model instantiation in a fresh Colab runtime (no training) to verify remote model compatibility, dataset schema, and dependencies.
2. Check the private training code's actual sampling, clipping, noise placement, and accountant assumptions; parsing alone cannot establish a DP guarantee.
3. Confirm each epsilon experiment starts from the intended pretrained initialization and does not accidentally reuse state from a previous budget.
4. Check all checkpoint directories and Google Drive mounts in the grader's environment; saved paths refer to the author's Drive.
5. Verify whether reported scores can be reproduced from saved model checkpoints; no checkpoints are included in this package.
6. Preserve the original full notebook as the historical experiment record. These curated extracts are not independently validated reproductions.

## Suggested safe verification order
Open the non-private notebook in a fresh GPU Colab, run only through dataset setup and model instantiation, then stop before the epoch loop. Repeat for DP-SGD and DP-SAT. Do not use Run All until the audit issues and privacy-accounting questions are resolved.
