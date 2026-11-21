# Clean promoter notebook extracts

These notebooks were curated from `DNABERT2_DP_Comparison.ipynb` and have **not** been executed end-to-end. They are starting points for reproduction, not certified push-button scripts.

1. `01_promoter_nonprivate_bitfit.ipynb`: non-private baseline.
2. `02_promoter_dp_sgd.ipynb`: original ε=8/4/2 training and diagnostic cells.
3. `03_promoter_dp_sat.ipynb`: original DP-SAT training cells ε=4/2/8 and audits.

Use Colab GPU, mount your own Drive, and verify `RESULTS_DIR`. Running training is optional if only inspecting results; it can take hours and create checkpoints. Some extracted cells assume original-session variables or hard-coded paths; the common setup provides primary aliases, but **manual preflight is still required**.

**Important:** The original DP-SGD cells were built in a different Colab session and use different dataset objects from later DP-SAT cells. The common setup intentionally reproduces the later data preparation; verify that this split is identical to the original DP-SGD experiment before comparing new runs. The original privacy claims, Poisson sampling, RNG and accountant choices require independent verification.

No notebook outputs were fabricated. Original source remains unchanged in GitHub.
