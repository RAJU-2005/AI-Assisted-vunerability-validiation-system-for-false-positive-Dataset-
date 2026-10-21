# AI-Based Vulnerability False-Positive Mitigation

## Dataset Overview

This repository uses a **synthetic vulnerability-scanner dataset** to develop and test an AI-based approach for identifying potential false positives in vulnerability scan findings.

**Important:** This dataset is artificially generated for experimentation. The CVE-style identifiers are randomly generated identifiers used for formatting only; they are **not verified real CVEs**, and the records should not be interpreted as real vulnerability reports or evidence of actual system exposure.

## Dataset File

- `synthetic_vuln_dataset.xlsx` — Excel workbook containing the dataset and a brief dataset description.
- Worksheet: `Dataset`
- Records: **10,000**
- Features/columns: **11**
- Target column: `Label`

## Columns

| Column | Description |
|---|---|
| `CVE` | Synthetic CVE-style identifier; not a verified real CVE. |
| `CVSS` | Simulated CVSS-like score, ranging from 4.0 to 10.0. |
| `Service` | Simulated service or application associated with the finding. |
| `Port` | Port associated with the simulated service. |
| `Version` | Simulated software version string. |
| `State` | Simulated scanner state: `vulnerable`, `patched`, or `not vulnerable`. |
| `QoD` | Simulated Quality of Detection (QoD) score, represented as a percentage-like value. |
| `Patch` | Indicates whether the record's simulated patch status is `Yes` or `No`. |
| `Config` | Simulated finding/configuration category, such as `Vulnerable`, `Safe`, or `Misconfigured (false signature match)`. |
| `Actual_status` | Synthetic reference status: `Confirmed` or `Not vulnerable`. |
| `Label` | Binary target label used for model experiments: `1` = confirmed vulnerability; `0` = not vulnerable / potential false positive. |

## Label Distribution

The dataset contains the following target-label distribution:

| Label | Meaning in this synthetic dataset | Records | Share |
|---:|---|---:|---:|
| `1` | Confirmed vulnerability (`Actual_status = Confirmed`) | 3,000 | 30% |
| `0` | Not vulnerable (`Actual_status = Not vulnerable`) | 7,000 | 70% |
| **Total** | | **10,000** | **100%** |

The classes are imbalanced, so model evaluation should report more than accuracy. Consider precision, recall, F1-score, confusion matrix, and (where appropriate) precision-recall AUC. For a false-positive mitigation use case, inspect false positives and false negatives separately: reducing false alarms should not come at the cost of missing genuine vulnerabilities.

## Intended Use

The dataset can support experiments such as:

- Exploring patterns in scanner-style findings.
- Building a baseline binary classification model.
- Testing data preprocessing, feature encoding, and evaluation workflows.
- Studying false-positive mitigation concepts using simulated scanner states, QoD, patch information, and configuration indicators.

## Limitations and Responsible Use

- **Synthetic data only:** records are not collected from real infrastructure or a real vulnerability scanner.
- **No real-world validation:** performance on this dataset does not establish performance on OpenVAS, Greenbone, or any production scanner.
- **CVE identifiers are placeholders:** do not use them to look up, report, or assert real vulnerabilities.
- **Potential feature leakage:** `State`, `Config`, and `Actual_status` may closely encode the target label. If these fields are used as input features, a model may appear highly accurate by learning information that would not be available at prediction time. Define the intended prediction-time inputs first, and exclude target-derived or post-verification fields from training features.
- **Not for operational security decisions:** do not use this dataset alone to confirm, dismiss, prioritize, or remediate real vulnerability findings.

For meaningful validation, test the approach on properly authorized, real scan data with verified ground-truth labels, while protecting sensitive infrastructure details.

## Suggested Citation / Attribution

If you use this dataset in a report or project, describe it as:

> *A synthetic vulnerability-scanner dataset created for experimentation with AI-based false-positive mitigation. The records and CVE-style identifiers are simulated and are not verified real-world vulnerability data.*

## License and Provenance

This README does not assign a license to the dataset. Add a license only if you have the rights to distribute the workbook and its contents.
