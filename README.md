# Analysis-of-raw-measurement-count-data
An R-based dynamic noise-filtering framework establishes data reliability thresholds based on instrument limits of detection (LOD) to eliminate false positives, extract Universal Reliable Taxa (URT), and map systemic uncertainty in high-throughput data via high-contrast heatmaps.
# System Reliability Map & Noise Filter (R Implementation)

[![License: MIT](https://shields.io)](https://opensource.org)

A robust analytical framework implemented in R to address false positives and sample-specific background noise in high-throughput sequencing datasets. 

Developed based on the methodology established by **Tatsuki Itagaki (2026)**, this pipeline maps systemic uncertainty by calculating dynamic cutoff values directly tied to measuring instrument performance.

## Key Features
* **LOD-Driven Thresholding**: Implements a strict `wt >= 100` & `INSTRUMENT_LOD >= 10` filtering logic as a necessary condition.

* **Vectorized Reliability Mapping**: Categorizes detected features across three distinct logical bands (`Reliable`, `Uncertain`, and `Undetected`).
* **Universal Reliable Taxa (URT) Extraction**: Automatically isolates consistently reliable signatures across all samples.
* **High-Contrast Visualization**: Outputs publication-ready system reliability heatmaps (`ITAGAKI_2_Reliability_Heatmap.pdf`).

## Academic Citation
If you utilize this software, logic, or threshold methodology in your research, please cite the following original works:

1. Itagaki, T. (2026).  DOI: [10.13140/RG.2.2.25054.19523](https://doi.org/10.13140/RG.2.2.25054.19523)
2. Itagaki, T. (2026).  DOI: [10.13140/RG.2.2.14987.86562](https://doi.org/10.13140/RG.2.2.14987.86562)

---

## Data Logic
The core engine segments data point reliability based on your instrument's Limit of Detection (**LOD**):


| Status | Code | Condition | Color |
| :--- | :---: | :--- | :---: |
| **Reliable** | `1` | Value $\ge \text{LOD} \times 10$ | Blue (`#2980B9`) |
| **Uncertain**| `0` | $\text{LOD} \le \text{Value} < \text{LOD} \times 10$ | Orange (`#F39C12`) |
| **Undetected**| `-1`| Value $< \text{LOD}$ | Gray (`#E5E8E8`) |

> ⚠️ **Note**: Samples yielding an `Uncertainty_Score` of exactly **0%** are automatically flagged as suspected absolute noise data.

---

## Usage

### Data Input Format
The script expects a standard matrix or dataframe named `Dataset` where:
* **Rows** represent unique sample identifiers (`Sample_ID`).
* **Columns** represent detected taxonomies or features (`Taxa`).

### Execution
Ensure your input matrix is loaded into your R environment as `Dataset`, then run the script:
```r
source("reliability_filter.R")
```

### Outputs
1. `ITAGAKI_2_Reliability_Heatmap.pdf`: A structured, sorted heatmap showing sorted taxa and status bands.
2. `FINAL SYSTEM RELIABILITY SUMMARY REPORT`: A vectorized summary data frame printed to the console containing sample-specific uncertainty tracking.

## License
This project is licensed under the MIT License - see the [LICENSE](https://opensource.org) page for details.
Copyright (c) 2026 Tatsuki Itagaki.

---

# This is something I gained only by acknowledging my defeat and reflecting on it. This system would not exist without my mentor (Norio Sugimoto) who taught me statistics.
