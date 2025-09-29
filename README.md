# README: CNOT Gate Count and Runtime Data Repository

This repository contains two primary sets of simulation data for analyzing quantum circuit construction methods: **Raw CNOT Gate Counts** and **Summary Runtime Metrics**. All files are organized into dedicated subdirectories.

***

## 1. File Inventory and Overview

The repository is structured with two main data directories: `/raw_cnot_counts` and `/summary_runtime`.

| Directory | File Name Prefix | Metric Type | Variable | Sample Size |
| :--- | :--- | :--- | :--- | :--- |
| `raw_cnot_counts/` | `RAW_CNOT_N_...json` (3 files) | **Raw CNOT Count** | $N$ (Vertices) | 1000 cases per point |
| `raw_cnot_counts/` | `RAW_CNOT_P_...json` (4 files) | **Raw CNOT Count** | $p$ (Density) | 1000 cases per point |
| `summary_runtime/` | `SUMMARY_RUNTIME_vs_N.json` | **Runtime (Summary)** | $N$ (Vertices) | 100 cases per point |
| `summary_runtime/` | `SUMMARY_RUNTIME_vs_P.json` | **Runtime (Summary)** | $p$ (Density) | 100 cases per point |

***

## 2. Raw CNOT Gate Count Data (`raw_cnot_counts/`)

These files provide the raw lists of **1000 CNOT counts** per data point and can be used to reproduce the averages and error bars for the primary cost metric plots.

### File Naming and Parameter Interpretation

| File Path | Variable | Method / Variation | Key Range |
| :--- | :--- | :--- | :--- |
| `raw_cnot_counts/RAW_CNOT_N_...json` | **N** (Vertices) | Graph-Builder, time-reversed-1, time-reversed-2 | Keys are strings **"20" through "80"**. |
| `raw_cnot_counts/RAW_CNOT_P_...json` | **P** (Edge Density) | Graph-Builder, time-reversed-1, time-reversed-2 | Keys are strings representing **percentage: "10" through "90"**. |
| `raw_cnot_counts/RAW_CNOT_P_Graph-Builder-ER.json` | **P** (Edge Density) | Graph-Builder-ER (Erdős–Rényi variant) | Keys are strings representing **percentage: "10" through "90"**. |

### Structure Details (Common to all 7 files)

* **Format:** Single JSON object (dictionary).
* **Keys (Strings):** Represent the parameter value ($N$ or $p$).
* **Values (Array of Integers):** Each key holds an array of **1000 raw CNOT gate counts** corresponding to the outcome of 1000 random cases for that specific key value.

To derive the plotted average for any point, calculate the mean of the 1000 integers in the corresponding array.

***

## 3. Summary Runtime Data (`summary_runtime/`)

These files contain pre-calculated summary statistics for the runtime metric, measured over a sample of **100 random cases**.

### File Naming and Parameter Interpretation

| File Path | Variable | Key Range |
| :--- | :--- | :--- |
| `summary_runtime/SUMMARY_RUNTIME_vs_N.json` | **N** (Vertices) | Keys are **$N$ values** (e.g., "20", "30", etc.). |
| `summary_runtime/SUMMARY_RUNTIME_vs_P.json` | **P** (Edge Density) | Keys are **$p$ percentage values** ($10, 15, 20, \dots, 90$). |

### Structure Details (Common to both files)

The structure is a single JSON object where the keys are the parameter values ($N$ or $p$). The values are nested objects containing the summary metrics for all three primary methods:

```json
{
  "[N or P value]": {
    "Graph Builder": {
      "average": [float],
      "std_dev": [float]
    },
    "Graph Builder+simplification": {
      "average": [float],
      "std_dev": [float]
    },
    "time-reversed-1": {
      "average": [float],
      "std_dev": [float]
    }
  }
}
```
***
## 4. Contact and Citation

If you use this data in your own work, please cite the following publication:

S. Ghanbari and H.-K. Lo, Cost-aware Photonic Graph State Generation: A Graphical Framework, arXiv (2025).

Please refer to the accompanying paper for full details on the simulation and methodology.
