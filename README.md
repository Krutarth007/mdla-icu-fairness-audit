# Unmeasured but Not Unbiased: Demographic Information Encoded in Clinical Missingness Patterns and Its Implications for Fairness in Critical Care Mortality Prediction

**Krutarth Patel · Phanindra Beedala**  

---

## Overview

This repository contains the complete analysis code, results tables, and 
output figures for the above manuscript. The analysis introduces the 
**Missingness Demographic Leakage Audit (MDLA)** — a four-step framework 
for detecting whether clinical measurement absence patterns encode 
demographic information that predictive models can exploit as a latent 
bias pathway.

---

## 📁 Repository structure
```
mdla-icu-fairness-audit/
│
├── README.md
├── requirements.txt
├── LICENSE
├── .gitignore
│
├── notebook/
    ├── fairness_audit_ICU_COMPLETE.ipynb
│
└── results/
    ├── figures/
    │   ├── fig2_missingness_heatmap.png
    │   ├── fig2_missingness_heatmap.pdf
    │   ├── fig3_demographic_leakage.png
    │   ├── fig3_demographic_leakage.pdf
    │   ├── fig4_calibration_curves.png
    │   ├── fig4_calibration_curves.pdf
    │   ├── fig5_fairness_dashboard.png
    │   ├── fig5_fairness_dashboard.pdf
    │   ├── fig6_subgroup_calibration_recal.png
    │   ├── fig6_subgroup_calibration_recal.pdf
    │   ├── fig7_pareto_frontier.png
    │   ├── fig7_pareto_frontier.pdf
    │   ├── fig8a_shap_global.png
    │   ├── fig8a_shap_global.pdf
    │   ├── fig9_race_stratified_shap.png
    │   ├── fig9_race_stratified_shap.pdf
    │   ├── fig10_missingness_shap_race.png
    │   ├── fig10_missingness_shap_race.pdf
    │   ├── fig11_group_dca.png
    │   └── fig11_group_dca.pdf
    │
    ├── tables/
    │   ├── table1_cohort_mimic.csv
    │   ├── table1_cohort_eicu.csv
    │   ├── table2_missingness_gaps.csv
    │   ├── table3_missingness_chi2_race.csv
    │   ├── table4_fairness_metrics.csv
    │   ├── table4b_fairness_gaps_ci.csv
    │   ├── table5_recalibration_comparison.csv
    │   ├── table5b_recalibration_external.csv
    │   ├── table6_tripod_ai.csv
    │   ├── table_ablation_missingness_indicators.csv
    │   ├── table_domain_shift_ks.csv
    │   ├── table_grouplatt_paradox.csv
    │   ├── table_missingness_leakage_summary.csv
    │   ├── table_missingness_leakage_summary_ci.csv
    │   ├── table_missingness_shap_by_race.csv
    │   ├── table_performance_internal.csv
    │   ├── table_performance_external.csv
    │   └── key_metrics_summary.json
    │
    └── cache/
        ├── mimic_features_raw.parquet
        ├── eicu_features_raw.parquet
        └── combined_pre_imputation.parquet
```

---

## Data access

This study uses two publicly available critical care databases. 
**Raw data is not included in this repository** per PhysioNet data use 
agreements. Access requires free registration and CITI training at 
[https://physionet.org](https://physionet.org).

| Database | Role | DOI |
|---|---|---|
| MIMIC-IV v2.2 | Development cohort (n=50,827) | https://doi.org/10.13026/6mm1-ek67 |
| eICU-CRD v2.0 | External validation (n=137,773) | https://doi.org/10.13026/C2WM1R |

The `results/cache/` directory contains derived aggregate feature matrices 
(Parquet format) that allow re-entry into the pipeline from the post-
extraction stage without reprocessing the full raw databases.

---

## Reproducing results

All results regenerate from the cached intermediate outputs. After cloning:

```bash
pip install -r requirements.txt
jupyter notebook fairness_audit_ICU_COMPLETE.ipynb
```

All random operations use a fixed seed (`seed=42`). Runtime from cache 
entry is approximately 15–25 minutes on a standard laptop CPU.

To run from raw data, place MIMIC-IV and eICU files in the paths 
specified in Section 1 of the notebook and re-run all cells from the top.

---

## Key results

| Metric | Value |
|---|---|
| MDLA race AUROC from missingness alone | 0.543 (95% CI: 0.540–0.546) |
| Bonferroni-significant race-missingness features | 18 / 43 |
| XGBoost internal AUROC | 0.910 (95% CI: 0.900–0.920) |
| XGBoost external AUROC | 0.799 (95% CI: 0.794–0.803) |
| Ablation racial AUROC disparity increase | +10.7% (0.063 → 0.069) |
| Global Platt ECE reduction (internal) | 94% (0.124 → 0.007) |
| Equalized-odds TPR gap (race) | 0.214 |

---

## Citation

If you use this code or the MDLA framework, please cite:

> Patel K, Beedala P. Unmeasured but Not Unbiased: Demographic Information 
> Encoded in Clinical Missingness Patterns and Its Implications for Fairness 
> in Critical Care Mortality Prediction. *Journal of the American Medical 
> Informatics Association*. 2026. [In review]

---

## License

MIT License. See `LICENSE` for details.  
Clinical data accessed under PhysioNet credentialed data use agreements.
