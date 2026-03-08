# DataGovernance_Group2
Data Governance and Ecosystem project in Nova SBE - Group 2
hi, julius first commit in readme
Hi, Constança first commit in readme


Data Governance and Ecosystem project in Nova SBE — Group 2

---

## Project Overview

NovaCred is a fintech startup that uses machine learning to make credit decisions. This project audits NovaCred's credit application dataset for data quality issues, algorithmic bias, and governance gaps.

---

## Repository Structure
```
project-team2/
├── data/                        # Raw and cleaned datasets
├── notebooks/
│   ├── 01-data-quality.ipynb    # Data quality analysis
│   ├── 02-bias-analysis.ipynb   # Bias detection & fairness
│   └── 03-privacy-demo.ipynb    # Privacy & GDPR compliance
├── presentation/                # Video or link
└── README.md
```

---

## Key Findings

### Data Quality
> To be completed by Data Engineer

### Bias Detection
- **Gender Disparate Impact: DI = 0.767** — below the legal 0.80 threshold (four-fifths rule violated)
- **Approved loan amount gap:** Female applicants receive on average $2 757 less than male applicants among approved cases
- **Age bias:** The 18-29 group has the lowest approval rate (41.5%)
- **ZIP code proxy:** Correlation between female ratio and approval rate = -0.94, strong indirect discrimination
- **Income does not explain the gap:** Female applicants have higher average income and longer credit history than males
- **DTI proxy:** Women in the lowest debt-to-income quartile (best financial profile) have a DI of 0.57, the most severe finding

### Privacy & Governance
> To be completed by Governance Officer

---

## Team

| Role | Member | Student ID |
|---|---|---|
| Data Engineer | — | - |
| Data Scientist | Constança Branco | 71059 |
| Governance Officer | — | - |
| Product Lead | Constança Branco  Julius  Petra |
