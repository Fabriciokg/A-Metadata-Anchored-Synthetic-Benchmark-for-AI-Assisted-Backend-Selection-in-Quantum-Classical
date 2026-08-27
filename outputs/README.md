# Published outputs

This directory contains the curated, reviewed open-science artifacts selected from the local benchmark output directory `outputs_ai_quantum_open_science/`.

Unlike transient local run directories, the files here are intended to be versioned so that readers can inspect the reported evidence without rerunning the complete notebook.

## Directory layout

```text
outputs/
├── README.md
├── MANIFEST.md
├── SHA256SUMS.txt
├── data/
│   └── README.md
├── figures/
│   └── anchor_alpha_distance_sensitivity.png
├── real_validation/
│   └── *.csv
└── tables/
    └── *.csv
```

## What each directory contains

- `tables/`: report-ready benchmark summaries, model metrics, ranking/regret results, grouped validation, ablations, subgroup analyses, sensitivity analyses, multi-seed robustness, IBM frozen-versus-live comparisons, and evidence-scope tables.
- `real_validation/`: external-metadata plausibility and validation-support artifacts, including the hardware-sanity protocol/status and metadata comparison files.
- `figures/`: selected figures exported by the benchmark.
- `data/`: reserved for deliberately published datasets. The current snapshot contains only a README because the supplied open-science export did not include raw pair-level data in this folder.

## Evidence scope

The dataset summary in `tables/final_dataset_description.csv` reports 700 workloads, 5 backend candidates, 3,500 workload-backend pairs, 6 algorithm profiles, and 6 decision profiles.

The frozen external-reference analysis uses an IBM/Qiskit Runtime snapshot dated 2026-07-28. A separate authenticated live metadata collection was recorded on 2026-08-26. The live collection summary states that credential values were not persisted and that the metadata-collection section submitted no hardware jobs.

The hardware sanity-check result is `skipped_by_default`. Therefore, these files must not be described as production-QPU validation.

The external range-overlap diagnostic is 37.5% for the frozen snapshot and 25.0% for the live comparison. These are descriptive metadata-level plausibility diagnostics, not model accuracy scores or global benchmark-validity percentages.

See `../docs/RESULTS_AND_EVIDENCE.md` for the recommended interpretation of these artifacts.

## Integrity

`SHA256SUMS.txt` contains a SHA-256 checksum for every published file in the output snapshot. `MANIFEST.md` provides a human-readable inventory.

The generated `tables/artifact_inventory.csv` is preserved as an original notebook artifact. Its `relative_path` column refers to the original local export directory (`outputs_ai_quantum_open_science/...`), not the final GitHub publication path.
