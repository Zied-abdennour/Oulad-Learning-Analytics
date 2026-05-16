# OULAD Learning Analytics — Comparative Data Preprocessing

Comparative analysis of the Open University Learning Analytics Dataset across three methodologies: classical preprocessing, LLM-assisted interpretation, and automated profiling.

---

## Project overview

| | |
|---|---|
| Dataset | Open University Learning Analytics Dataset (OULAD) |
| Records | 32,593 enrolment records across 7 linked CSV files |
| VLE interactions | 10,655,280 click-level records |
| Methods compared | 3 (classical, LLM, automated profiling) |
| Final dataset | 32,593 rows × 48 columns |

---

## Methods

### 1. Classical preprocessing (`notebooks/01_classical_preprocessing.ipynb`)
Reproducible pandas pipeline covering missing value handling, IQR-based outlier flagging, enrolment-level feature engineering, categorical encoding, and export of a model-ready master dataset.

### 2. LLM-assisted analysis (`reports/02_LLM_Report.pdf`)
12 structured prompts sent to an LLM with verified OULAD summaries as evidence. The LLM role was interpretation only — bias detection, fairness warnings, and educational meaning. No raw computation. Each prompt card documents the prompt used, evidence supplied, LLM output, and reliability control.

### 3. Automated profiling (`notebooks/03_automated_profiling.ipynb`)
ydata-profiling HTML reports generated for all 7 raw OULAD files plus aggregated VLE features. studentVle.csv (10M rows) was sampled at 100,000 rows for the raw scan, then profiled at enrolment level after aggregation.

---

## Key findings

| Finding | Value |
|---|---|
| Overall pass rate | 47.2% |
| Strongest pass predictor | Assessment submissions submitted (r = 0.71) |
| Average VLE clicks — Withdrawn | 314 |
| Average VLE clicks — Distinction | 2,667 |
| Pass rate — no disability | 48.2% |
| Pass rate — disability disclosed | 38.1% |
| Missing imd_band values | 1,111 (3.41%) — preserved as Unknown |

---

## Where the three methods agreed and conflicted

**Agreed:**
- Enrolment key must be `code_module` + `code_presentation` + `id_student`, not `id_student` alone
- Missing `imd_band` is a fairness issue, not just a data quality issue
- VLE engagement rises consistently from Withdrawn → Fail → Pass → Distinction

**Conflicted:**
- Outliers: IQR flags them; LLM argues high clicks may reflect real learning behaviour, not noise
- Binary target: useful for modelling, but hides the difference between Withdrawn and Fail
- Demographic gaps: descriptive statistics show them; LLM frames them as support signals, not ability labels

---

## Repo structure

```
oulad-learning-analytics/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── 01_classical_preprocessing.ipynb
│   └── 03_automated_profiling.ipynb
├── reports/
│   ├── 02_LLM_Report.pdf
│   └── 03_FinalReport.pdf
└── data/
    └── .gitkeep
```

---

## How to run

```bash
git clone https://github.com/Zied-abdennour/oulad-learning-analytics
cd oulad-learning-analytics
pip install -r requirements.txt
```

Download the dataset from the [OULAD page](https://analyse.kmi.open.ac.uk/open-dataset) and place all 7 CSV files in `data/raw/`.

Run notebooks in order:
```
notebooks/01_classical_preprocessing.ipynb
notebooks/03_automated_profiling.ipynb
```

The LLM report is a standalone PDF (`reports/02_LLM_Report.pdf`) documenting all 12 prompts, supplied evidence, outputs, and reliability controls.

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
scikit-learn
ydata-profiling
jupyter
```

---

## Dataset

OULAD is publicly available from the Open University Knowledge Media Institute.  
Direct download: https://analyse.kmi.open.ac.uk/open-dataset

The 7 files used: `courses.csv`, `assessments.csv`, `studentAssessment.csv`, `studentInfo.csv`, `studentRegistration.csv`, `vle.csv`, `studentVle.csv`

---

## Authors

Zied Abdennour,Youssef Ghorbel, Mohamed Hedi Benrhouma
