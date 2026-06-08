# X-CheckList: Explanation-Grounded Behavioral Testing and Counterfactual Validation for NLP Model Failure Diagnosis

X-CheckList is a research-oriented diagnostic framework for analyzing NLP model failures beyond simple pass/fail accuracy. It combines behavioral test construction, attribution-based evidence, counterfactual validation, EVFS severity scoring, and human-readable failure reason inference.

## Project Focus

This project targets reliable and explainable NLP evaluation. Instead of only reporting whether a model prediction is wrong, X-CheckList asks: **why did the model fail, which cues were ignored or overused, and how severe is the failure?**

## Key Contributions

- Explanation-validated failure diagnosis for NLP classification models.
- Attribution-aware failure analysis using occlusion, gradient-based attribution, and integrated gradients.
- Counterfactual validation for testing whether model behavior changes under controlled input perturbations.
- EVFS scoring for ranking failure severity.
- Human-readable failure reason inference for diagnostic reporting.
- Baseline comparison against Standard CheckList, CheckList + Attribution, and CheckList + Counterfactual variants.

## Supported Tasks and Models

**Datasets:** SST-2, IMDB, MNLI, SNLI, QQP, MRPC  
**Models:** DistilBERT, BERT, RoBERTa  
**Tasks:** Sentiment classification, natural language inference, paraphrase detection  
**Explanation Methods:** Occlusion, gradient, integrated gradients

## Main Run Summary

| Metric | Value |
|---|---:|
| Run mode | full |
| Successful runs | 17 |
| Total test cases | 1886 |
| Total result rows | 5351 |
| Total failed cases | 1222 |
| Overall failure rate | 22.84% |
| Mean AM | 0.1169 |
| Mean CS | 0.0381 |
| Mean EVFS | 0.0081 |

## Capability-Level Summary

| Capability | Total Tests | Failed Tests | Failure Rate | Mean AM | Mean CS | Mean EVFS |
|---|---:|---:|---:|---:|---:|---:|
| word_order_sensitivity | 15 | 14 | 93.33% | 0.707 | 0.091 | 0.665 |
| lexical_overlap | 24 | 18 | 75.00% | 0.554 | 0.094 | 0.490 |
| semantic_role_sensitivity | 1800 | 735 | 40.83% | 0.204 | 0.000 | 0.000 |
| contradiction | 24 | 8 | 33.33% | 0.277 | 0.666 | 0.277 |
| semantic_equivalence | 1500 | 268 | 17.87% | 0.089 | 0.000 | 0.000 |
| robustness | 1800 | 165 | 9.17% | 0.046 | 0.032 | 0.005 |
| entity_invariance | 44 | 4 | 9.09% | 0.063 | 0.007 | 0.001 |
| negation | 120 | 10 | 8.33% | 0.067 | 0.888 | 0.054 |
| temporal_sentiment | 24 | 0 | 0.00% | 0.000 | 0.851 | 0.000 |

## Top Diagnostic Failure Groups

| Dataset | Model | Capability | Relation | Failure Rate | Mean EVFS |
|---|---|---|---|---:|---:|
| mnli | bert | contradiction | directional | 100.00% | 0.831 |
| snli | bert | contradiction | directional | 100.00% | 0.831 |
| mrpc | bert | word_order_sensitivity | directional | 100.00% | 0.752 |
| mrpc | roberta | word_order_sensitivity | directional | 100.00% | 0.747 |
| snli | roberta | lexical_overlap | directional | 100.00% | 0.746 |

## Human Evaluation Summary

| Method | Correctness | Understandability | Usefulness | Actionability | Overall Mean |
|---|---:|---:|---:|---:|---:|
| X-CheckList | 5.000 | 4.000 | 4.387 | 4.320 | 4.427 |
| CheckList + Counterfactual | 4.000 | 4.920 | 3.840 | 3.813 | 4.143 |
| CheckList + Attribution | 4.000 | 4.000 | 3.453 | 3.307 | 3.690 |
| Standard CheckList | 4.000 | 4.960 | 2.000 | 2.000 | 3.240 |

## Repository Structure

```text
X-CheckList/
├── README.md
├── requirements.txt
├── .gitignore
├── config/
│   └── xchecklist_config.json
│
├── notebooks/
│   └── X_CheckList_Main_Experiment.ipynb
├── figures/
│   ├── baseline_comparison.png
│   ├── failure_rate_by_capability.png
│   ├── mean_evfs_by_capability.png
│   ├── model_dataset_failure_heatmap.png
│   └── top_diagnostic_capabilities_evfs.png
├── results/
│   ├── xchecklist_aggregate_report.csv
│   ├── xchecklist_instance_report.csv
│   ├── xchecklist_failed_cases.csv
│   ├── baseline_comparison_report.csv
│   ├── ablation_report.csv
│   ├── human_evaluation_results.csv
│   └── other result files


```

## Installation

```bash
pip install -r requirements.txt
```

For GPU-based experiments, install a PyTorch build compatible with your CUDA version from the official PyTorch installation page.

## How to Run

Open the notebook:

```text
notebooks/X_CheckList.ipynb
```

Then run the cells in order. The notebook is designed around a configuration-first workflow. If you run it locally or on Colab, update paths in the configuration cell or `config/xchecklist_config.json` as needed.

## Reproducing / Inspecting Existing Results

The repository already includes generated reports under `results/` and figures under `figures/`. To print a compact summary from the included result files, run:

```bash
python scripts/summarize_results.py
```

## Important Notes

- Large raw datasets and model checkpoints are not included.
- Put external datasets in `data/` only if your license permits redistribution.
- Do not commit private API keys, Hugging Face tokens, or local machine paths.
- The notebook output has been cleared for a clean GitHub view.

## Technologies Used

Python, PyTorch, Hugging Face Transformers, datasets, scikit-learn, pandas, NumPy, Matplotlib, Captum, NLP model evaluation, attribution analysis, and counterfactual evaluation.

## Suggested GitHub Topics

`nlp`, `explainable-ai`, `model-evaluation`, `llm-evaluation`, `counterfactual-evaluation`, `responsible-ai`, `pytorch`, `huggingface`


