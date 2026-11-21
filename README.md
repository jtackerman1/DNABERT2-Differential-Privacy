# DNABERT-2 Differential Privacy Comparison

## Project Overview

This project evaluates the privacy–utility tradeoffs of fine-tuning DNABERT-2, a genomic DNA foundation model, using differentially private training methods.

The primary objective is to compare non-private Bias-Term Fine-Tuning (BiTFiT), Differentially Private Stochastic Gradient Descent (DP-SGD), and a DP-SAT-style training approach on genomic core-promoter classification.

The experiments evaluate classification accuracy at three target privacy budgets (ε = 2, 4, and 8), along with loss-based membership inference attacks to examine potential privacy leakage.

This research was completed as part of a graduate data privacy research project at the University of North Carolina at Charlotte.

## Research Questions

1. Can DP-SGD be applied to bias-only fine-tuning of DNABERT-2 while maintaining useful classification accuracy?
2. How does DP-SAT-style training compare with standard DP-SGD under similar privacy budgets?
3. What do loss-based membership inference attacks reveal about the evaluated models?

## Dataset and Model

**Foundation model:** [DNABERT-2-117M](https://huggingface.co/zhihan1996/DNABERT-2-117M)

**Dataset:** [Genomic Understanding Evaluation (GUE)](https://huggingface.co/datasets/leannmlindsey/GUE)

Primary task: `prom_core_all` — binary DNA core-promoter classification.

- Training samples: 42,620
- Validation samples: 4,736
- Test samples: 5,920

A secondary exploratory experiment used `splice_reconstructed` for three-class splice-site classification.

## Experimental Setup

| Configuration | Value |
|---|---|
| Foundation model | DNABERT-2-117M |
| Fine-tuning approach | BiTFiT |
| Private methods | DP-SGD, DP-SAT-style |
| Privacy budgets | ε = 2, 4, 8 |
| Delta | 1e-5 |
| Gradient clipping norm | 1.0 |
| Batch size | 8 |
| Training epochs | 3 (primary comparison) |
| Random seed | 42 |
| GPU | NVIDIA Tesla T4 |
| Environment | Google Colab |
| Privacy accounting | Rényi Differential Privacy |

## Experimental Results

### Core-Promoter Classification

| Method | Privacy Budget | Test Accuracy |
|---|---|---|
| Non-private BiTFiT | N/A | 80.27% |
| DP-SGD | ε = 2 | 76.54% |
| DP-SGD | ε = 4 | 76.30% |
| DP-SGD | ε = 8 | 76.08% |
| DP-SAT-style | ε = 2 | 74.56% |
| DP-SAT-style | ε = 4 | 76.91% |
| DP-SAT-style | ε = 8 | 76.96% |

The non-private baseline achieved the highest accuracy.

DP-SAT-style training performed slightly better than DP-SGD at ε = 4 and ε = 8, while DP-SGD performed better at ε = 2.

These results represent single-seed experimental runs. Small accuracy differences should not be interpreted as statistically significant.

### Membership Inference

A loss-based membership inference attack was evaluated against the non-private and private models.

ROC-AUC scores were approximately 0.50 across the evaluated configurations, including the non-private baseline.

These findings indicate that the evaluated attack did not effectively distinguish training members from nonmembers. They do not establish that the models are immune to stronger privacy attacks.

## Repository Structure

**Original research notebook**

`DNABERT2_DP_Comparison.ipynb`

Contains the original Google Colab experimental development, training, evaluations, and exploratory work. It is retained as an archival research record and is not intended to be executed sequentially.

**Curated experiment notebooks**

- `notebooks/01_promoter_nonprivate_bitfit.ipynb` — Non-private BiTFiT baseline.
- `notebooks/02_promoter_dp_sgd.ipynb` — DP-SGD experiments.
- `notebooks/03_promoter_dp_sat.ipynb` — DP-SAT-style experiments.

These notebooks separate the main experimental methods for easier inspection. They have not been independently verified through a complete fresh-runtime execution.

**Results and figures**

- `final_research_results.csv` — Final reported experimental results.
- `final_research_summary.json` — Research results summary.
- `method_comparison.csv` — Comparison of training methods.
- `combined_mia_results.csv` — Membership inference results.
- `figure1_privacy_utility.png` — Privacy–utility comparison.
- `figure2_membership_inference.png` — Membership inference visualization.
- `figure3_dpsat_advantage.png` — DP-SAT accuracy differences.

Additional analysis exports are retained in the repository.

## Reproducing the Experiments

### 1. Prepare the Environment

Use Google Colab with a GPU-enabled runtime, preferably an NVIDIA Tesla T4 or comparable GPU.

Clone the repository:

```bash
git clone https://github.com/jtackerman1/DNABERT2-Differential-Privacy.git
cd DNABERT2-Differential-Privacy
```

Install the listed dependencies:

```bash
pip install -r requirements.txt
```

### 2. Obtain the Dataset and Model

The notebooks reference the publicly available GUE dataset and pretrained DNABERT-2 model from Hugging Face.

The repository does not redistribute these large resources.

### 3. Review the Experiment Notebooks

Open the notebooks in Google Colab in the following order:

1. `01_promoter_nonprivate_bitfit.ipynb`
2. `02_promoter_dp_sgd.ipynb`
3. `03_promoter_dp_sat.ipynb`

Review the setup, dataset paths, and runtime dependencies before execution. The curated notebooks are research extracts, not independently validated one-click reproduction scripts.

### 4. Inspect the Results

The provided CSV, JSON, and figure files allow the reported results to be reviewed without retraining the foundation model.

Re-running private training may require substantial GPU computation.

## Reproducibility and Limitations

- Results were obtained using a single random seed.
- The original research notebook contains exploratory and debugging cells.
- The curated notebooks have not been validated end-to-end in a clean runtime.
- Privacy accounting depends on the sampling and training implementation assumptions.
- The specific DP-SAT-style implementation has not undergone independent formal privacy verification.
- Experimental pseudorandomness should not be treated as cryptographically secure.
- Membership inference results near random guessing do not prove the absence of privacy leakage.
- Model checkpoints and large datasets are not included in this repository.

Additional provenance and limitations are documented in `SOURCE_AND_LIMITATIONS.md`.

## Author

Jason Ackerman  
University of North Carolina at Charlotte  
Graduate Research Project — 2026
