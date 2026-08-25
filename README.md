# The Mid-Career Valley

**Replication data, survey instrument, and analysis code for the study:**

> Hossain, M. A. *The Mid-Career Valley: Uncovering a Non-Linear Relationship Between Work Experience and Entrepreneurial Intention Among Salaried Employees in a South Asian Emerging Economy.*

This repository contains all datasets, materials, and code required to independently reproduce every result, table, figure, and robustness check reported in the manuscript. It is provided in support of the peer-review process for *Humanities and Social Sciences Communications*.

---

## Overview

The study tests whether work experience exerts a **non-linear (U-shaped) effect** on entrepreneurial intention (EI) among salaried employees, using a cross-sectional survey of **1,001 respondents** across ten occupational sectors in Bangladesh. Analyses include hierarchical polynomial regression, parallel bootstrap mediation, moderation, moderated mediation, and nine systematic robustness checks. All analysis is fully scripted and reproducible from the files below.

---

## Repository Contents

| File | Description |
|------|-------------|
| `Jobs Dataset.csv` | The complete, anonymized survey dataset (n = 1,001). Contains all raw response items and the variables used in analysis. |
| `The Mid-Career Valley, Questionnaire.pdf` | The full survey instrument as administered to respondents, including all items, response scales, and instructions. |
| `The_Mid_Career_Valley.ipynb` | The complete, executable analysis notebook (Python 3.12). Runs end-to-end from the raw CSV to every reported statistic and figure. |

---

## Mapping to the Editorial Technical-Check Requirements

This section maps the repository contents directly to the materials requested in the editorial technical check.

| Requested material | Location in this repository |
|--------------------|-----------------------------|
| **Data files (raw and processed)** | `Jobs Dataset.csv` — the raw survey data. All processing (mean-centering, quadratic-term construction, composite scoring, recoding) is performed transparently inside `The_Mid_Career_Valley.ipynb`, so the processed data can be regenerated deterministically from the raw file. |
| **Survey instruments and protocols** | `The Mid-Career Valley, Questionnaire.pdf` — the full questionnaire and data-collection instructions. |
| **Variable details (definitions, coding, transformations)** | See the [Variables and Coding Scheme](#variables-and-coding-scheme) section below, and the inline documentation in the notebook. |
| **Analysis resources (scripts, code, formulae)** | `The_Mid_Career_Valley.ipynb` — all statistical procedures and figure-generation code. |
| **Supporting documentation** | This README, together with the notebook's inline commentary. |

---

## Variables and Coding Scheme

**Dependent variable**

- **Entrepreneurial Intention (EI)** — three-item composite (Cronbach's α = .829), each item on a 5-point Likert scale (1 = Strongly Disagree, 5 = Strongly Agree):
  1. Frequency of thinking about starting one's own business or project
  2. Plans to start a venture in the future
  3. Whether concrete steps toward independence have already been taken

**Primary predictor**

- **Work Experience** — collected as five ordinal categories and encoded numerically (1–5) for polynomial regression:
  `0–2 years = 1`, `3–5 years = 2`, `6–10 years = 3`, `11–15 years = 4`, `16+ years = 5`.
  The encoded variable is **mean-centered** (`exp_c`) prior to squaring (`exp_c²`) to reduce multicollinearity between the linear and quadratic terms.

**Mediators** (single-item, 5-point Likert)

- **Psychological Safety** — adapted from Edmondson (1999)
- **Growth Mindset** — adapted from Dweck (2016)
- **Risk Appetite** — willingness to accept risk in pursuit of independence

**Moderators**

- **Gender** — Male / Female
- **Employment Type** — Permanent / Contract / Part-time / Freelance (permanent vs. non-permanent used in moderation tests)

**Controls**

- Education level, marital status, and sector (ten categories; dummy-coded with Garments as the reference group).

> **Note for reviewers:** Exact column headers in `Jobs Dataset.csv` are read and labelled at the top of the notebook. All recoding steps that translate raw column values into the analysis variables above are shown explicitly in the code, so no transformation is hidden.

---

## Reproducing the Analysis

**Requirements**

- Python 3.12
- `statsmodels`, `numpy`, `scipy`, `matplotlib`, `scikit-learn`, `pandas`

**Setup**

```bash
# Clone the repository
git clone https://github.com/Alamgir-JUST/The-Mid-Career-Valley.git
cd The-Mid-Career-Valley

# (Recommended) create and activate a virtual environment
python3.12 -m venv venv
source venv/bin/activate          # On Windows: venv\Scripts\activate

# Install dependencies
pip install statsmodels numpy scipy matplotlib scikit-learn pandas jupyter
```

**Run**

```bash
jupyter notebook The_Mid_Career_Valley.ipynb
```

Execute the cells in order. The notebook reads `Jobs Dataset.csv` from the repository root and reproduces, in sequence:

1. Measurement quality assessment (Cronbach's α, Harman's single-factor test)
2. Descriptive statistics and the Pearson correlation matrix
3. One-way ANOVA with post-hoc Tukey HSD across the five experience groups
4. Hierarchical polynomial regression (Models 1–3) testing the quadratic effect (**H1**)
5. Parallel mediation with 5,000 bootstrap iterations (**H2a–c**)
6. Gender and employment-type moderation (**H3, H4**)
7. Moderated mediation and the Index of Moderated Mediation (**H5**)
8. All nine robustness checks
9. Generation of Figures 2–6

All bootstrap procedures use 5,000 resamples. Random seeds are set in the notebook so that bootstrap confidence intervals are exactly reproducible.

---

## Ethical Approval

Ethical approval was granted by the **Skill Morph Ethics Committee** (Approval No. SkillMorph/ES/2025/09(03), 3 September 2025). The study followed the ethical principles of the Declaration of Helsinki. Participation was voluntary, informed consent was obtained from all respondents, no personally identifiable information was collected, and anonymity and confidentiality were maintained throughout. The dataset in this repository is fully anonymized.

---

## Data Availability Statement

*(This statement is also included at the end of the manuscript.)*

The datasets, survey instrument, and complete analysis code generated and analyzed in this study are openly available in this GitHub repository:
**https://github.com/Alamgir-JUST/The-Mid-Career-Valley**

Specifically, the repository provides: the anonymized survey dataset (`Jobs Dataset.csv`); the full survey instrument (`The Mid-Career Valley, Questionnaire.pdf`); and the complete, executable analysis notebook containing all data-preprocessing, hierarchical polynomial regression, parallel mediation with bootstrap resampling, moderation, moderated-mediation, robustness-check, and figure-generation code (`The_Mid_Career_Valley.ipynb`). All analyses were conducted in Python 3.12 using openly available libraries (statsmodels, numpy, scipy, matplotlib, scikit-learn). No third-party or proprietary data or software were used. No restrictions apply to the availability of these materials.

---

## Citation

If you use these materials, please cite the article (full bibliographic details to be added upon publication):

```
Hossain, M. A. (2025). The Mid-Career Valley: Uncovering a Non-Linear Relationship
Between Work Experience and Entrepreneurial Intention Among Salaried Employees in a
South Asian Emerging Economy. [Manuscript submitted for publication].
```

---

## Author

**Md. Alamgir Hossain**
Department of Computer Science and Engineering, State University of Bangladesh, Dhaka, Bangladesh
Skill Morph Research Lab., Skill Morph, Dhaka, Bangladesh

- Email: alamgir.cse14.just@gmail.com
- ORCID: [0000-0001-5120-2911](https://orcid.org/0000-0001-5120-2911)

---

## License

Unless otherwise stated, the materials in this repository are made available for the purposes of academic review, replication, and non-commercial research. Please contact the author regarding any other use.
