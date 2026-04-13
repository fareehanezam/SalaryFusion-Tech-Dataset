# SalaryFusion-Tech
This dataset is constructed by merging and harmonizing 3 independent compensation sources: Stack Overflow Developer Survey (2023), Levels.fyi Salary Data (2018–2021), and Glassdoor Job Postings (~2019–2020) and standardized into a single schema for analysis and modeling.

---

The records were cleaned and aligned into one common format with shared columns such as salary, experience, role, company, location, education, and skills.

This is best described as a **curated multi-source dataset**, not a newly collected raw dataset.

## Dataset Size

- **Rows:** 107,005
- **Columns:** 14

---

## Columns

| Column | Description |
|---|---|
| `salary` | Normalized salary value used for analysis |
| `log_salary` | Natural log of `salary` |
| `original_salary` | Original salary value before normalization |
| `experience` | Years of experience, when available |
| `education` | Education level, when available |
| `role` | Job title or role |
| `company` | Company name, when available |
| `location` | Geographic location |
| `industry` | Industry or sector, when available |
| `skills_structured` | Structured skills field, when available |
| `skills_text` | Unstructured skills text, mostly from Glassdoor |
| `data_source` | Source of the record (`stack_overflow`, `levels_fyi`, `glassdoor`) |
| `sample_weight` | Weight used to help balance sources during modeling |
| `salary_within_source_zscore` | Z-score of salary within each source |


---

## Quick Start

```python
import pandas as pd

df = pd.read_csv("employee_salary_dataset_final.csv")

print(df.head())
print(df.columns)
````

---

## Notes on Processing

The dataset was processed to make the sources comparable:

- Different source schemas were aligned into one shared format
- Text fields were standardized
- Salary values were normalized for consistency
- Source imbalance was handled using inverse-frequency sample weights
- A within-source z-score was added for modeling and comparison

## Example Use Cases

- Salary prediction
- Compensation analysis
- Feature engineering experiments
- Cross-source comparison studies
- Domain adaptation / transfer learning

## Important Notes

- Some columns are missing for some rows because not every source provides the same information.
- The dataset should be treated as a **mixed-source, cleaned benchmark dataset**, not as a single original survey.
- I do not claim that this dataset is novel in the sense of new raw data collection; the novelty is in the **combination, cleaning, and standardization**.

---

## Limitations & Practical Considerations

While the dataset is cleaned and standardized, users should be aware of the following:

- **Missing Data:**  
  `skills_text` (~99% missing), `industry` (~75%), `education` & `skills_structured` (~57%), and `company` (~43%) contain significant missing values.

- **Source Imbalance:**  
  Uneven distribution across sources (Levels.fyi ~60K, Stack Overflow ~45K, Glassdoor ~457) may introduce bias. Use `sample_weight` during modeling.

- **High Cardinality:**  
  `location` (~1200+) and `role` (~300) have many unique values and require careful encoding.

- **Outliers:**  
  Experience values exceed 60+ years and salary ranges widely (4K–500K+), which may impact modeling.

- **Target Variable Recommendation:**  
  `log_salary` is preferred over `salary` for better distribution and model stability.

---  

## Data Sources

### 1. Stack Overflow Developer Survey 2023

* Source: [https://survey.stackoverflow.co](https://survey.stackoverflow.co/datasets/stack-overflow-developer-survey-2023.zip)
* Coverage: ~89,000 respondents (global)
* Used: ~46,000 records after filtering
* Salary: `ConvertedCompYearly` (USD)
* Strengths: Global diversity, skills, education
* Limitations: Self-reported, no company data
* Assigned Year: 2023

---

### 2. Levels.fyi Salary Data (2018–2021)

* Source: [https://www.levels.fyi](https://www.levels.fyi)
* Dataset repo: [https://github.com/Yashas-153/Data-Science-Stem-Salaries](https://github.com/Yashas-153/Data-Science-Stem-Salaries)
* Used: ~61,000 records
* Salary: total compensation (base + stock + bonus)
* Strengths: High-quality US tech compensation
* Limitations: US-dominant, equity-heavy salaries
* Year Range: 2018–2021

---

### 3. Glassdoor Job Postings Dataset

* Source repo: [https://github.com/PlayingNumbers/ds_salary_proj](https://github.com/PlayingNumbers/ds_salary_proj)
* Used: ~450–700 records (after filtering)
* Salary: Parsed from ranges (e.g., `$53K–$91K`)
* Strengths: Industry + job descriptions
* Limitations: Small size, estimated salaries
* Assigned Year: ~2019–2020

---

## Repository Structure

```
employee_salary_dataset.ipynb
employee_salary_dataset_final.csv
README.md
LICENSE
```

---

## Data Usage Notice

This dataset is derived from publicly available sources:

* Stack Overflow
* Levels.fyi
* Glassdoor

Users must comply with original source licenses when using this dataset.

---

## Citation

```bibtex
@dataset{employee_salary_dataset,
  title   = {SalaryFusion-Tech},
  url     = {https://github.com/fareehanezam/SalaryFusion-Tech-Dataset}
}
```

---

## License

This dataset is released under the MIT License.

You are free to use, modify, and distribute this dataset for any purpose, including commercial use, without restriction. Attribution is appreciated but not required.

---

## Contributing

Issues and pull requests are welcome.
Please report data inconsistencies with justification.

---

## Changelog

| Version | Date | Notes           |
| ------- | ---- | --------------- |
| v1.0.0  | 2026 | Initial release |

---
```
```
