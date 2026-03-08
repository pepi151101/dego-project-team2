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
- **PII pseudonymisation:** Full names tokenised (TKN-XXXXXX), emails hashed with SHA-256 + salt, SSNs masked (***-**-XXXX), IP addresses reduced to subnet (192.168.\*.\*)
- **Special category data (GDPR Art. 9):** Gambling spend and adult entertainment flagged as sensitive — collapsed into a single binary `red_flag_spending` column; raw values excluded from model
- **Data minimisation (GDPR Art. 5(1)(c)):** Date of birth reduced to age bucket (18-25, 26-35, …); IP address collection flagged as potentially unnecessary
- **Accuracy & retention (GDPR Art. 5(1)(d)(e)):** 59 records exceed the 2-year retention window; 2 records carry future-dated timestamps (2026, 2027); 438/500 records missing timestamps entirely
- **Automated decision-making (GDPR Art. 22):** Gender DI of 0.767 and intersectional DI of 0.548 for women aged 18-29 constitute discriminatory automated decisions
- **Data protection by design (GDPR Art. 25):** No ingestion validation in place — implausible and stale records entered the pipeline unchecked
- **Data breach risk (GDPR Art. 33):** 7 applicants approved with no verifiable identity on file; 4 with missing SSN
- **EU AI Act violations:** Bias unmitigated pre-deployment (Art. 9); training data stale and inaccurate (Art. 10); 438 decisions unlogged and unauditable (Art. 12); flagged records never routed for human review (Art. 14)


## Team

| Role | Member |
|---|---|
| Data Engineer | — |
| Data Scientist | Constança Branco |
| Governance Officer | — |
| Product Lead | — |
