# LLM Annotation Reliability

**Is LLM self-consistency a usable signal for routing annotation work?**

This repository contains the code and experimental pipeline for evaluating whether self-consistency and verbalised confidence from Large Language Models (LLMs) can reliably predict annotation correctness for Polish persuasion and manipulation techniques.

## Repository Structure

```text
llm-annotation-reliability/
├── data/
│   ├── MIPD/                        # MIPD dataset splits (train, validation, test) # [Git-ignored] Raw MIPD dataset files (local only)
│   ├── SemEval23/                   # Polish subset of SemEval-2023 Task 3 # [Git-ignored] Raw SemEval-2023 Task 3 Polish files (local only)
│   └── results/
│       └── poc_gemma3_results.csv   # Proof-of-Concept model outputs and confidence signals
├── scripts/
│   ├── eda.ipynb                    # Exploratory Data Analysis (raw dataset statistics and label distributions)
│   ├── POC.ipynb                    # Proof-of-Concept inference pipeline (greedy + 5 stochastic reruns)
|   └── POC_metric.ipynb             # Proof-of-Concept visualization of metrics
├── .env                             # Local environment variables (API keys, excluded from Git)
├── pyproject.toml                   # Project dependencies and configuration
└── uv.lock                          # Locked environment dependencies (uv)
```

# **Datasets**:
   * **MIPD** (`data/MIPD/`): Polish manipulation techniques dataset (CC BY-NC-ND 4.0).
   * **SemEval-2023 Task 3** (`data/SemEval23/`): Polish persuasion techniques dataset (restricted research access; not redistributed in the public repository).

## Important Note on Data Distribution:

Raw datasets are not distributed in this repository due to licensing constraints described in our Phase-1 Data Statement:

* SemEval-2023 Task 3 (Polish subset) [RESTRICTED]: Distributed by the task organisers upon request under terms of use that strictly prohibit redistribution or sharing with third parties.

* MIPD (Manipulation and Intention in Polish Disinformation) [CC BY-NC-ND 4.0]: Publicly available for non-commercial research directly from the authors' repository at github.com/ArkadiusDS/MIPD.

To run the notebooks locally, place the obtained dataset files into the following paths expected by the scripts:

data/MIPD/ — train.csv, validation.csv, test.csv

data/SemEval23/ — Polish subtask 3 training and development text/label files (train-labels-subtask-3.txt, dev-labels-subtask-3.txt, and corresponding .template files)

## Notebooks Overview

* **`scripts/eda.ipynb`**: Raw Exploratory Data Analysis of the MIPD and SemEval-2023 Task 3 datasets
* **`scripts/POC.ipynb`**: End-to-end Proof-of-Concept generation pipeline using `google/gemma-3-12b-it`. For each sampled article, the script collects $1$ greedy reference output ($T=0.0$) and $5$ stochastic outputs ($T=0.7$, $\text{top-}p=0.95$) with fixed seeds to compute the majority decision, self-consistency, and verbalised confidence. The raw results are saved to `data/results/poc_gemma3_results.csv` for downstream metric evaluation.

## Authors

* Mikołaj Twardowski
* Aleksandra Idczak
* Kacper Wnęk