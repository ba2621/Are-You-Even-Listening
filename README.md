
# **Are You Even Listening?**

### *Measuring Prompt Reliance Across Instruction-Tuning Datasets*

This repository contains the full code, experiments, and reports for our COMS 4705 NLP project, **“Are You Even Listening?”**—a systematic investigation into how Large Language Models distribute attention across different segments of an instruction-tuned input.

##  Project Goal

We study **prompt reliance** by measuring how LLaMA-2-7B distributes attention toward:

* **P — System / prompt instructions**
* **U — User query**
* **A — Assistant prior outputs (chat history)**

By analyzing the *post-softmax attention weights* across all layers and heads, we quantify how much each token segment influences the model’s next-token generation.

---

##  Repository Structure

### **`week1/` — Dataset Setup & Tokenization**

Contains all preprocessing and segmentation work:

* **Selected dataset construction** (`selected_all_shuffled.jsonl`)
* **Tokenizer & chat-template implementation using LLaMA-2-7B**
* **Unified P/U/A segmentation logic**
* **Automatic metadata extraction** (token spans, lengths, distribution)
* **Behavioral heuristic labeler**
* **End of Week 1 report**

Key files:

* `NLP_Project_Tokenizer_Llama_2_7b_chat_hf.ipynb`
* `Behavioral_Heuristic_Labeler.ipynb`
* `Dataset Setup Report (End of Week 1).pdf`

---

### **`week2/` — Attention Extraction Pipeline**

Implements the model-instrumentation pipeline required to compute:

* **PAM** — Prompt Attention Mass
* **QAM** — Query Attention Mass
* **SAM** — Self-Attention Mass

Work includes:

* TransformerLens attention hooks
* Verified token-to-segment back-mapping
* Layer × head attention extraction
* Diagnostic plots and normalization checks
* Preliminary correlation between attention scores and instruction-following behavior

---

### **`weekX/` (future weeks)**

Will include:

* PCL (Prompt-Conditioned Loss) experiments
* Cross-model comparison (Mistral-7B, LLaMA-3)
* Final research paper + slides

---

##  Datasets

We use a unified sample drawn from:

* **Alpaca**
* **FLAN**
* **ShareGPT** (heavy filtering required due to extremely long contexts)

*Note:* ShareGPT contains extreme cases (e.g., 24k-token users, 9.6k-token assistants).
For models limited to 4096 tokens, we will either:

1. **Drop over-length examples**, or
2. **Truncate U/A to the last N tokens** (e.g., 1500 each) and recompute spans.

---

##  Current Progress

✔ Complete dataset selection & cleaning
✔ Implemented tokenizer + segmentation metadata
✔ Verified P/U/A boundaries for all datasets
✔ Built attention-extraction pipeline
✔ Captured sample PAM/QAM/SAM values
✔ Delivered Week 1 report

Next steps:

* Apply dataset truncation rule to ShareGPT
* Run full batch attention extraction
* Compute aggregate metrics per dataset
* Prepare mid-semester deliverable slides

---

##  Team

* **Israel (Researcher 2)** 
* **Benny (Researcher 1)** 
* **Arsh (Researcher 3)**

---


