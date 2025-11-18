

#  **Week 1 — Dataset Setup & Behavioral Heuristic Labeling**

*NLP Project: “Are You Even Listening?”*

This folder contains all deliverables for **Week 1** of the project.
The goal of Week 1 was to establish a clean dataset pipeline, verify tokenizer behavior, build heuristic labels, and prepare the foundation for Week 2 attention extraction.

---

##  **1. Goals for Week 1**

* Build a **minimal shared dataset spec** (JSONL format)
* Identify and segment:

  * `system_text`
  * `user_text`
  * `assistant_prior_text`
* Run the **LLaMA-2–7B-Chat tokenizer** to confirm tokenization alignment
* Produce **behavioral heuristic labels** for instruction-following behavior
* Generate a **shuffled, clean Week 1 dataset**
* Begin preliminary organization for **attention extraction** (Week 2)

---

##  **2. Files Included**

### ** Notebooks**

| File                                             | Description                                                                                           |
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| `Behavioral_Heuristic_Labeler.ipynb`             | Implements heuristic labeling logic for “followed vs. ignored instructions” using P/U/A segmentation. |
| `NLP_Project_Tokenizer_Llama_2_7b_chat_hf.ipynb` | Tests tokenization behavior, segment boundaries, and validates JSONL schema.                          |
| `Attention_Datasets.ipynb`                       | Early work collecting attention outputs + dataset structuring for Week 2.                             |
| `Dataset Setup Report (End of Week 1).pdf`       | Week 1 report summarizing progress, methodology, and next steps.                                      |

---

### ** Dataset Files**

| File                          | Description                                                          |
| ----------------------------- | -------------------------------------------------------------------- |
| `selected_all_shuffled.jsonl` | Final cleaned and shuffled dataset for Week 1.                       |
| `attention_*` (if present)    | Early attention-format datasets produced during exploratory testing. |

---

##  **3. JSONL Schema (Shared Spec)**

Each dataset entry uses the agreed-upon schema:

```json
{
  "id": "datasetName:uniqueId",
  "dataset": "alpaca|flan|sharegpt",
  "raw_prompt": "...",
  "system_text": "...",
  "user_text": "...",
  "assistant_prior_text": "...",
  "constraint_tags": ["length_limit", "format_json", "persona", ...]
}
```

This schema is **locked across teammates** to keep our pipelines compatible.

---

##  **4. Heuristic Labeling (Week 1 Deliverable)**

Week 1 uses lightweight behavioral heuristics to classify:

* Whether assistance followed constraints
* Whether the model respected format/tone rules
* Whether the output violated explicit instructions
* Whether system role / persona was preserved

These labels are preliminary and will be compared to **attention-based alignment scores** in Week 3.

---

##  **5. Tokenizer Verification**

We ran controlled tests using:

```
meta-llama/Llama-2-7b-chat-hf
```

to verify:

* Proper segmentation into **P/U/A** regions
* Clean token-level alignment
* Ability to map tokens back to raw text
* Stability of system + user tokens across samples

This ensures Week 2 attention extraction will be structurally correct.

---

##  **6. How This Sets Up Week 2**

Week 1 deliverables directly support Week 2 pipelines:

* The **clean JSONL dataset** is ready for attention hooks
* Segment boundaries are verified for token-to-text mapping
* Heuristic labels will serve as ground truth for early correlations with:

  * PAM (Prompt Attention Metric)
  * QAM (Question Attention Metric)
  * SAM (Self Attention Metric)

---

##  **7. Next Steps (For Week 2)**

* Implement post-softmax attention hooks
* Extract layer-/head-wise attention for a subset of samples
* Compute PAM/QAM/SAM
* Plot attention heatmaps
* Build correlation table: attention vs. instruction-following behavior

---


