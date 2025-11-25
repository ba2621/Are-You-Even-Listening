
# **Week 3 — Researcher 2: Behavior Correlation Analysis**

Below is the complete structure and organization for the Week-3 Researcher-2 deliverables. This document explains:

1. **Folder structure**
2. **Which files to upload**
3. **How to organize your part of the repository**
4. **A full explanation of the Researcher-2 role**

This matches the format of Week-1 and Week-2 already in the repository.

---

#  1. Folder Structure for Week-3

Create the following folders in your GitHub repository:

```
Week 3 - Metrics/
    Researcher 2 - Behavior Correlation/
```

This keeps your work parallel to **Researcher 1 – Metrics Developer**.

---

#  2. Files to Upload (Researcher 2 Output)

Upload **all** of the following into:

```
Week 3 - Metrics/Researcher 2 - Behavior Correlation/
```

### **Core Outputs**

| File                                            | Description                                        |
| ----------------------------------------------- | -------------------------------------------------- |
| **merged_metrics_with_labels.parquet**          | Final dataset merging R1 metrics + behavior labels |
| **correlation_results.csv**                     | Pearson + Spearman correlations for PAM/QAM/SAM    |
| **Week3_Researcher2_BehaviorCorrelation.ipynb** | Your complete Colab notebook                       |

### **Figures**

Upload all 4 PNGs:

* `PAM_layer_heatmap.png`
* `PAM_norm_scatter.png`
* `QAM_norm_scatter.png`
* `SAM_norm_scatter.png`

### **Optional (recommended for reproducibility)**

Inside:

```
Week 3 - Metrics/Researcher 2 - Behavior Correlation/data/
```

Upload:

* **behavior_labels.csv**

---

#  3. Final GitHub Repo Structure (Correct & Professional)

```
Are-You-Even-Listening/
│
├── Week 1 - data preparation/
│
├── Week 2 - Attention hooks pipeline/
│
└── Week 3 - Metrics/
      ├── Researcher 1 - Metrics Developer/
      │     ├── metrics.py
      │     ├── all_metrics.parquet
      │     ├── all_metrics_NORMALIZED.parquet
      │     ├── layer_summary.csv
      │     ├── head_summary.csv
      │     ├── Week3_MetricsDeveloper_R1.ipynb
      │     └── data/
      │           └── (R1 outputs)
      │
      └── Researcher 2 - Behavior Correlation/
            ├── Week3_Researcher2_BehaviorCorrelation.ipynb
            ├── merged_metrics_with_labels.parquet
            ├── correlation_results.csv
            ├── PAM_layer_heatmap.png
            ├── PAM_norm_scatter.png
            ├── QAM_norm_scatter.png
            ├── SAM_norm_scatter.png
            └── data/
                  └── behavior_labels.csv
```

This mirrors your team roles exactly and is fully aligned with project requirements.

---

#  4. README (Place Inside the R2 Folder)

Copy/paste the text below into:

**`Week 3 - Metrics/Researcher 2 - Behavior Correlation/README.md`**

---

# **Researcher 2 — Behavioral Correlation Analysis (Week 3)**

My Week-3 role was to connect the **attention metrics computed by Researcher 1** (PAM, QAM, SAM) with the **behavioral labels defined in Week-2**. The goal is to quantify whether a model’s attention patterns predict helpful or harmful behavior.

---

## **1. Loading Metrics + Behavior Labels**

I loaded:

* `all_metrics_NORMALIZED.parquet` (from Researcher 1)
* `behavior_labels.csv` (from Week-2)

Then I merged them using the shared `id` field to create:

* **merged_metrics_with_labels.parquet**

This file is the unified dataset for all correlation work.

---

## **2. Computing Correlation Metrics**

For **every dataset × layer × head**, I computed:

### Pearson correlations

* PAM_norm ↔ behavior_label
* QAM_norm ↔ behavior_label
* SAM_norm ↔ behavior_label

### Spearman correlations

* PAM_norm ↔ behavior_label
* QAM_norm ↔ behavior_label
* SAM_norm ↔ behavior_label

### Filtering rule

Only include a layer/head if **both labels** {0, 1} appear.

All results are saved in:

* **correlation_results.csv**

---

## **3. Visualization Outputs**

I generated four figures that summarize how attention relates to behavior:

1. **PAM Pearson Heatmap by Layer**
2. **Scatter: PAM_norm vs behavior_label**
3. **Scatter: QAM_norm vs behavior_label**
4. **Scatter: SAM_norm vs behavior_label**

These help visualize positive/negative correlation trends across datasets and layers.

---

## **4. Final Merged Dataset**

The final merged dataset is:

* **merged_metrics_with_labels.parquet**

It contains:

* dataset
* id
* layer/head indices
* normalized attention metrics
* behavioral label
* correlations-ready fields
