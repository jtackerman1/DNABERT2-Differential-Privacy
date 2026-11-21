# Source and Limitations

## Research Provenance

The original research experiments were developed in Google Colab and are preserved in `DNABERT2_DP_Comparison.ipynb`.

Three curated notebooks are provided in the `notebooks/` directory to separate the non-private BiTFiT, DP-SGD, and DP-SAT-style experiments.

The repository also contains exported experimental results in CSV and JSON formats, along with figures used to visualize the privacy–utility comparisons.

The original notebook and exported results are retained as research records. The curated notebooks have not been independently executed end-to-end in a fresh runtime.

## Experimental Scope

The primary experiments evaluate DNABERT-2 on the GUE core-promoter classification dataset using non-private BiTFiT, DP-SGD, and DP-SAT-style training at target privacy budgets of ε = 2, 4, and 8.

A secondary exploratory experiment evaluates splice-site classification. The private splice experiment was limited to DP-SGD at ε = 8 and did not improve beyond majority-class prediction. A full private comparison across methods was not completed for this secondary task.

## Research Limitations

1. **Reproducibility:** The curated notebooks may require environment configuration, updated file paths, and GPU resources. They have not been verified through a complete fresh-runtime execution.

2. **Privacy accounting:** The reported privacy budgets rely on Rényi Differential Privacy accounting and the training implementation's sampling assumptions. The DP-SAT-style implementation has not undergone independent formal privacy verification.

3. **Randomness:** Experimental pseudorandom number generation was used for reproducibility and should not be considered cryptographically secure.

4. **Statistical significance:** The reported comparisons use a single random seed. Small accuracy differences between methods should not be interpreted as statistically significant.

5. **Membership inference:** Loss-based membership inference attacks produced ROC-AUC scores near 0.50, including for the non-private baseline. These results do not establish that the models are immune to privacy attacks.

6. **Result verification:** Some DP-SGD evaluation values were consolidated from previously recorded experiments and were not independently reconstructed from saved checkpoints.

7. **Large artifacts:** The repository does not redistribute pretrained model weights, raw datasets, or trained checkpoints. The model and datasets are available from their respective public sources.

## Reproducibility Resources

- Original Colab research notebook: `DNABERT2_DP_Comparison.ipynb`
- Curated experiment notebooks: `notebooks/`
- Dependencies: `requirements.txt`
- Final reported results: `final_research_results.csv`
- Research summary: `final_research_summary.json`
- Membership inference results: `combined_mia_results.csv`

The repository provides the code, methodology, recorded experimental results, and documentation necessary to inspect the research. Full independent reproduction requires additional runtime configuration and computational resources.
