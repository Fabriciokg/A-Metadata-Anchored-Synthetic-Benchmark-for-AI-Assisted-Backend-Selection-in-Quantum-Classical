# Results and evidence scope

This document explains how to interpret the curated artifacts committed under `outputs/`.

## 1. Benchmark scope

The reported experiment is a controlled synthetic benchmark for AI-assisted backend selection in quantum-classical workflows. Synthetic workloads, backend candidates, operational outcomes, recommendation labels, and utility targets are used to evaluate learning and decision strategies under controlled conditions.

The published dataset description reports:

- 700 workloads;
- 5 backend candidates;
- 3,500 workload-backend pairs;
- 6 algorithm profiles;
- 6 decision profiles.

These counts are recorded in `outputs/tables/final_dataset_description.csv`.

## 2. External metadata evidence

Two external metadata contexts are represented in the published output.

### Frozen reproducibility reference

The canonical frozen IBM/Qiskit Runtime reference is dated 2026-07-28. It is represented in the published anchor-reference and frozen-plausibility tables, including:

- `outputs/tables/final_qpu_generation_anchor_reference.csv`;
- `outputs/tables/final_metadata_vs_synthetic_frozen_plausibility_ranges.csv`;
- `outputs/tables/final_metadata_vs_synthetic_frozen_plausibility_summary.csv`.

This frozen reference supports reproducible metadata anchoring for the reported experiment. It does not turn the synthetic benchmark into a production execution-log dataset.

### Live comparison

The published live metadata table contains three IBM backends collected on 2026-08-26. Related artifacts include:

- `outputs/tables/final_external_qpu_metadata.csv`;
- `outputs/tables/final_ibm_live_collection_summary.csv`;
- `outputs/tables/final_ibm_frozen_vs_live_common_backend_drift.csv`;
- `outputs/tables/final_ibm_frozen_vs_live_distribution_summary.csv`;
- `outputs/tables/final_metadata_vs_synthetic_live_plausibility_summary.csv`.

The live collection summary records `credential_values_persisted=False` and `hardware_jobs_submitted_by_this_section=False`.

## 3. External-plausibility percentages

The frozen-reference summary reports:

- range-overlap metrics: 37.5%;
- metrics with external reference: 8;
- metrics without external reference: 8;
- mean synthetic values within reference ranges: approximately 37.07%.

The live-comparison summary reports:

- range-overlap metrics: 25.0%;
- metrics with external reference: 8;
- metrics without external reference: 8;
- mean synthetic values within reference ranges: approximately 32.46%.

These percentages are descriptive range-overlap plausibility diagnostics at the metadata level. They are not model-accuracy scores, not percentages of real-world validation, and not measures of overall benchmark validity.

## 4. Hardware-execution status

`outputs/real_validation/hardware_sanity_results.csv` records the hardware sanity check as `skipped_by_default` and explains that the open-science execution avoids credentialed hardware usage unless explicitly enabled.

Accordingly, the current published evidence should not be described as:

- production-QPU validation;
- a production-ready scheduler evaluation;
- evidence of quantum advantage;
- real-world superiority over production scheduling systems.

Appropriate wording includes "synthetic benchmark partially anchored in IBM/Qiskit Runtime metadata", "metadata-level external-plausibility analysis", and "controlled methodological evaluation".

## 5. Predictive and selection results

The committed summary tables include holdout regression, classification, ranking, and regret metrics. For example, the primary backend-ranking summary reports Top-1 accuracy of 0.55, Top-2 accuracy of approximately 0.807, and Top-3 accuracy of 0.95 for the reported holdout selection evaluation.

The utility-regret summary reports mean regret of approximately 0.0136 and an exact backend match rate of 0.55 for that evaluation.

These values characterize recovery of the benchmark's synthetic policy under the specified evaluation design. They do not establish production scheduling optimality.

## 6. Multi-seed robustness

The multi-seed summary contains 10 benchmark realizations. The mean selection Top-1 value is approximately 0.566, with the reported 95% confidence interval spanning approximately 0.533 to 0.600. The same table reports robustness summaries for classification, runtime regression, fidelity regression, and utility regret.

The multi-seed results are intended to test whether conclusions depend strongly on a single synthetic random seed.

## 7. Information access and baseline interpretation

`outputs/tables/final_review_information_access_taxonomy.csv` distinguishes strategies according to the information available at test time and during training. In particular, direct learned-utility comparators use the synthetic utility target during training, while other strategies use operational criteria, learned acceptability gating, explicit policy weights, or unweighted multicriteria rules.

Because these strategies receive different information and optimize different targets, comparisons should be interpreted descriptively rather than as perfectly symmetric head-to-head competitions.

## 8. Integrity and reproducibility

Use `outputs/SHA256SUMS.txt` to verify that published artifacts have not changed. The human-readable `outputs/MANIFEST.md` lists each committed output file, its size, and checksum.

The notebook-generated `outputs/tables/artifact_inventory.csv` is preserved without rewriting its original local relative paths, so that provenance from the original export remains visible.
