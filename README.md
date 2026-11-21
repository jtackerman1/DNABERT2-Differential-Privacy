DNABERT-2 Differential Privacy Comparison
Research reproducibility materials for the GUE core-promoter classification comparison of non-private BiTFiT, DP-SGD, and DP-SAT, with exploratory splice-site experiments.
Status
Starter archive — not yet a one-click reproducible release. The original notebook is included unchanged, with historical debugging, runtime-dependent state, and Google Drive paths. Do not execute all cells sequentially. Before a final release, extract validated scripts and confirm each experiment's exact execution path and privacy assumptions.
Source datasets and pretrained model
- GUE: https://huggingface.co/datasets/leannmlindsey/GUE — prom_core_all, splice_reconstructed
- DNABERT-2: https://huggingface.co/zhihan1996/DNABERT-2-117M
The repository intentionally does not redistribute pretrained weights, datasets, or trained checkpoints.
Contents
- notebooks/original/: unchanged uploaded Colab notebook (archival reference, not clean execution order)
- results/promoter/: supplied final-analysis CSV and JSON exports
- figures/: supplied figures
- docs/: data provenance and reproducibility limitations
- requirements.txt: key pinned dependencies observed in notebook; Colab/PyTorch versions vary
Promoter results (reported test accuracy)
Method	epsilon	Accuracy
Non-private BiTFiT	—	0.8027
DP-SGD	2	0.765372
DP-SGD	4	0.763007
DP-SGD	8	0.760811
DP-SAT	2	0.745608
DP-SAT	4	0.769088
DP-SAT	8	0.769595


Source: results/promoter/final_research_results.csv.
Known limitations
- Results represent a single random seed.
- Loss-based membership inference ROC-AUC near 0.5 is not proof of privacy.
- DP-SAT privacy proof and implementation-specific privacy accounting require verification.
- Some DP-SGD test accuracy figures were carried forward from prior recorded evaluations; cross-check against raw logs/checkpoints before publication.
- The notebook includes unsuccessful experiments and exploratory splice-site training; these must be labeled distinctly from the final promoter comparison.
- Experimental pseudorandom number generation must not be described as cryptographically secure.
Reproduction plan (not yet validated)
Use a CUDA-equipped Google Colab runtime; install pinned model compatibility packages, fetch the public dataset/model, then execute separately validated non-private, DP-SGD, DP-SAT and evaluation entrypoints. The original notebook is retained to support extraction and auditing. Full training is compute-intensive and not required to inspect the provided results.# DNABERT2-Differential-Privacy-
DNABERT2-Differential-Privacy
