# Reproducibility notes

This repository contains a reproducible notebook for generating a synthetic benchmark for AI-assisted backend selection in quantum-classical workflows.

The benchmark is reproducible in structure, but some external metadata can change over time because IBM Quantum backends, calibration data, queue status, and account access are dynamic.

---

## Recommended execution information to report

When running the notebook, record:

- execution date and time;
- Python version;
- operating system;
- package versions;
- Qiskit version;
- qiskit-aer version;
- qiskit-ibm-runtime version;
- whether IBM metadata collection succeeded;
- number of IBM backends available to your account;
- whether hardware execution was disabled or enabled;
- generated output directory;
- random seed configuration, if modified.

---

## Deterministic and non-deterministic components

### Controlled components

The following parts are controlled by the notebook design:

- synthetic workload generation;
- synthetic backend catalog generation;
- workload-backend pairing;
- synthetic utility function;
- recommendation labels;
- train/test grouping by workload ID;
- regression, classification, ranking, and baseline evaluation logic.

### Dynamic components

The following parts may vary over time:

- IBM backend availability;
- IBM backend calibration metadata;
- IBM backend status;
- queue depth;
- account permissions;
- accessible IBM Quantum instances;
- installed package versions.

---

## Why results may differ slightly

Results can differ slightly across machines or dates because of:

- different package versions;
- different IBM metadata snapshots;
- different accessible IBM backends;
- stochastic model training behavior;
- different CPU/OS numerical behavior;
- notebook modifications.

These differences do not invalidate the benchmark. They should be reported when publishing or comparing results.

---

## Suggested reporting template

```text
Execution date:
Python version:
Operating system:
qiskit version:
qiskit-aer version:
qiskit-ibm-runtime version:
IBM metadata available: yes/no
Number of external superconducting backends:
Hardware execution enabled: yes/no
Output directory:
Notes:
```

---

## Expected output directory

The notebook writes artifacts to:

```text
outputs_ai_quantum_v9_6/
```

This folder may include:

- CSV files;
- JSON summaries;
- figures;
- tables;
- model predictions;
- ranking outputs;
- validation summaries.

Generated outputs are not committed by default because they can be reproduced by running the notebook.
