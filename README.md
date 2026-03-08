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
├── presentation/                
└── README.md
```

---

## Key Findings

---

### Data Quality
#### Notebook 01 — Data Quality Assessment & Cleaning Pipeline

> Audits 502 raw credit applications across 6 data quality dimensions, remediates 15 issues, and exports a clean dataset with a full audit trail.

**Input:** `data/raw_credit_applications.json` (502 records)  
**Output:** `data/cleaned_credit_applications.csv` (500 records × 39 columns) · `data/data_quality_report.json`

#### Design Principles

Every fix follows the same three-step pattern throughout the notebook:
1. **Preserve** — original value kept in a `_raw` column (e.g. `gender_raw`, `annual_income_raw`)
2. **Fix** — correction applied to a new clean column (e.g. `gender`, `annual_income`)
3. **Flag** — boolean flag marks every affected row (e.g. `income_imputed`, `dti_flag`)

Nothing is silently overwritten. The full audit trail is always preserved.

#### Issues by Dimension

| # | Dimension | Issue | Records | Action |
|---|-----------|-------|---------|--------|
| 1 | Uniqueness | Duplicate `_id` rows | 2 | Removed — `drop_duplicates(keep='first')` → 502 to 500 records |
| 2 | Consistency | Inconsistent gender coding (`M`/`F` vs `Male`/`Female`) | 111 | Standardised via `GENDER_MAP` lookup dictionary |
| 3 | Consistency | Mixed date formats (`YYYY-MM-DD`, `YYYY/MM/DD`, `DD/MM/YYYY`) | 161 | Custom `parse_date_of_birth()` parser → ISO 8601 |
| 4 | Validity | `annual_income` stored as text string | 8 | `pd.to_numeric(errors='coerce')` → `float64` |
| 5 | Validity | Negative `credit_history_months` | 2 | `.abs()` applied — `-10` → `10`, `-3` → `3` |
| 6 | Validity | `debt_to_income` = 1.85 (impossible — must be 0–1) | 1 | Divided by 10 → `0.185` (decimal point shift) |
| 7 | Completeness | Missing `annual_income` | 5 | Median imputation (~$81K) + `income_imputed` flag |
| 8 | Completeness | Missing `date_of_birth` | 4 | Flag only (`dob_missing`) — no PII fabrication |
| 9 | Completeness | Missing `email` | 7 | Flag only (`email_missing`) — no PII fabrication |
| 10 | Completeness | Missing `ssn` | 5 | Flag only (`ssn_missing`) — no PII fabrication |
| 11 | Completeness | Missing `processing_timestamp` | 438 | Flag only (`timestamp_missing`) — 87.6% of dataset |
| 12 | Accuracy | Cross-field logic violations | 5 | 4 granular flags added — no auto-correction |
| 13 | Accuracy | Conflicting SSNs across different applicants | 2 | `ssn_conflict` flag — potential fraud escalated to compliance |
| 14 | Timeliness | Impossible timestamps (before 2020 or after audit date) | 2 | `timestamp_implausible` flag |
| 15 | Timeliness | Stale records older than 24 months | 59 | `timestamp_stale` flag — GDPR Art. 5(1)(e) deletion required |


---

#### Output Columns

Each field in the output CSV comes in up to three forms:

| Type | Example | Purpose |
|------|---------|---------|
| Clean | `gender`, `annual_income` | Used in all downstream analysis |
| Raw | `gender_raw`, `annual_income_raw` | Original source value — audit trail |
| Flag | `income_imputed`, `dti_flag` | Marks every row that was touched or is incomplete |

`data_quality_report.json` is consumed directly by **Notebook 02** (Bias Analysis) and **Notebook 03** (Governance & Privacy Audit).

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
| Data Engineer | Julius Caspar | 74455 |
| Data Scientist | Constança Branco | 71059 |
| Governance Officer | — | - |
| Product Lead | Constança Branco  Julius Caspar  Petra |
