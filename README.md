# Are You Even Listening?

Quantifying how a chat-tuned LLM allocates attention across:
- `P`: system prompt tokens
- `U`: latest user query tokens
- `A`: prior assistant/context tokens

This repository contains the full project artifacts for the COMS 4705 final report:
`Are You Even Listening? Quantifying Prompt, User, and Assistant Attention Dynamics.pdf`.

Below is a general pictorial overview of our process:

![PHOTO-2025-12-04-15-30-03](https://github.com/user-attachments/assets/48b00200-4ef4-4035-aabc-6821343cc224)

## Project Summary

The project introduces three attention-mass metrics computed from post-softmax attention:
- `PAM` (Prompt Attention Mass): attention from answer tokens to `P`
- `QAM` (Query Attention Mass): attention from answer tokens to `U`
- `SAM` (Self-Context Attention Mass): attention from answer tokens to `A`

The analysis uses LLaMA-2-7B-Chat with TransformerLens and studies whether these metrics relate to instruction-following / safety behavior.

From the paper workflow in this repo:
- Initial curated pool: `300` examples (`100` each from Alpaca, FLAN, ShareGPT)
- After context-length filtering for 4096-token limit: `266` examples
  - `alpaca: 100`, `flan: 100`, `sharegpt: 66`

## Main Findings (from final report)

- Synthetic single-turn datasets (Alpaca/FLAN) show high prompt reliance but weak attention-behavior linkage.
- ShareGPT shows more structured mid/late-layer QAM/SAM patterns with modest predictive signal.
- Prompt-intervention experiments suggest:
  - Hard-harm refusal behavior is largely invariant across prompt framings.
  - In ambiguous regimes (borderline safety, civility, structural constraints), weaker safety framing yields more direct but less cautious outputs.

See full methodology/results in:
- `Are You Even Listening? Quantifying Prompt, User, and Assistant Attention Dynamics.pdf`

## Repository Map

- `Data Preparation/`
  - Dataset curation, tokenization checks, heuristic behavior labeling notebooks
  - Key dataset files:
    - `selected_all_shuffled.jsonl` (300 rows)
    - `selected_all_tokenized.jsonl` (300 rows)

- `Attention Hooks Pipeline/`
  - Span verification and attention extraction notebooks
  - Key outputs:
    - `token_segmentation_metadata.json` (300 examples; includes `input_ids`, `p_span`, `u_span`, `a_span`)
    - `attention_metrics.jsonl` (266 examples; per-example layer/head metric payloads)

- `Metrics/`
  - Week 3 metric aggregation and behavior-correlation artifacts
  - Key outputs:
    - `all_metrics.parquet` (`280,896` rows; includes per-head plus `head='avg'` rows)
    - `all_metrics_NORMALIZED.parquet` (`280,896` rows)
    - `layer_summary.csv` (`96` rows)
    - `head_summary.csv` (`3,072` rows)
  - Behavior correlation/prediction subfolders include merged datasets, correlations, ROC plots, and model summaries.

- `Week5/`
  - Prompt-intervention and embedding-space analysis artifacts
  - Key outputs:
    - `llama_embeddings.npy` (`132 x 4096`)
    - `key_directions.npz` (compliance/divergent directions)
    - Labeled evaluation CSVs across regimes (`hard_harm`, `borderline`, `civility/constraints`, `neutral`)

- `FinalOutput/`
  - Consolidated notebooks and exported figures/files used for final deliverables.

## Data/Artifact Notes

- Most of the project is notebook-driven (`.ipynb`) rather than packaged Python scripts.
- `Metrics/metrics.py` is currently a placeholder file, so the authoritative metric pipeline in this repo is in notebooks/artifacts under `Metrics/` and `FinalOutput/`.
- Some filenames include spaces and duplicate suffixes like `(1)`, `(2)` from notebook export/versioning.

## Reproduction (Notebook-First)

Because this repo is notebook-centric, run the analysis in stages:

1. Data preparation
- `Data Preparation/NLP_Project_Tokenizer_Llama_2_7b_chat_hf.ipynb`
- `Data Preparation/Behavioral_Heuristic_Labeler.ipynb`

2. Span verification + attention extraction
- `Attention Hooks Pipeline/segmentation_metadata.ipynb`
- `Attention Hooks Pipeline/Attention Extraction.ipynb`

3. Metric summaries + correlations + prediction
- `Metrics/Week3_MetricsDeveloper_R1 (1).ipynb`
- `Metrics/Behavior Data Collection/Week3_Researcher2_BehaviorCorrelation.ipynb`
- `Metrics/Behavior Predictor/Week3_Researcher3_BehaviorPredictor (1).ipynb`

4. Prompt intervention / embedding analysis
- `Week5/FianlWeek5Experiments (1).ipynb`
- `Week5/PCA_Analysis_Week_5 (1).ipynb`

## Environment

No lockfile/environment file is committed. Based on notebook imports, typical dependencies include:
- `torch`, `transformers`, `transformer_lens`
- `pandas`, `numpy`, `scipy`, `scikit-learn`
- `matplotlib`, `seaborn`, `tqdm`, `datasets`, `jsonlines`

Model/tokenizer references in notebooks use:
- `meta-llama/Llama-2-7b-chat-hf`

## Citation

If you use this repository, cite the report:
- `Are You Even Listening? Quantifying Prompt, User, and Assistant Attention Dynamics.pdf`

## Authors

- Benny Attar
- Avi Maslow
- Arsh Misra
