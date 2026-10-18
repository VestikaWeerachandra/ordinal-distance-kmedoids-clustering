# Comparing Distance Measures for Ordinal Data in K-Medoids Clustering

**Segmenting hotel guests in Sri Lanka by their perceptions of service features**

HNDDS final research project | National Innovation Centre (NIBM), Colombo | Supervisor: Mr. Ashan Arthanayake
**Author:** Vestika Weerachandra

<img src="https://raw.githubusercontent.com/VestikaWeerachandra/ordinal-distance-kmedoids-clustering/main/results/figures/distance_measure_comparison_silhouette.png" width="600" alt="Silhouette comparison">

## Overview

Hotel guest ratings (Unacceptable to Excellent) are **ordinal**, yet clustering often uses distance measures that assume interval-scaled data. This project asks: *which ordinal-appropriate distance measure gives the most valid and interpretable guest segments in K-Medoids (PAM) clustering?*

I compared three measures on 3,230 guest reviews covering 161 hotels and 12 nationalities in Sri Lanka (2024-2025), provided by House of Travels \& Tourism (Pvt) Ltd:

1. **Gower distance**
2. **Podani's ordinal extension of Gower** (rank-based, tie-corrected)
3. **Walesiak's GDM2** (built for ordinal item-battery data)

## Key findings

|Distance measure|Best k|Silhouette|Davies-Bouldin (approx.)|
|-|-|-|-|
|Gower|2|0.5991|0.9645|
|Podani|2|0.6321|0.9870|
|**GDM2**|**2**|**0.6352**|0.9654|

* **GDM2 produced the best-defined clusters** (highest Silhouette). All three measures pointed to two segments, but the segment boundaries differed: 70/30 (Gower), 68/32 (Podani), 61/39 (GDM2). The choice of distance measure changes who ends up in which segment.
* **Two guest segments with GDM2:** *Highly Satisfied* (60.9%, median "Excellent" on every feature) and *Moderately Satisfied* (39.1%, median "Good" on every feature).
* **Segments differ significantly on all six features and Overall Rating** (Kruskal-Wallis, p < 0.001) with large effect sizes (epsilon-squared 0.44 to 0.65).
* **Dining drives the split:** Quality Meals and Restaurant Service show the biggest gaps between segments (Top-Box gaps of 29.4 and 25.3 points). Check-in and staff friendliness separate the segments least.

<img src="https://raw.githubusercontent.com/VestikaWeerachandra/ordinal-distance-kmedoids-clustering/main/results/figures/kruskal_wallis_effect_size_ranked.png" width="600" alt="Effect sizes">

## Business takeaway

Hotels and the tour operator get the most leverage on overall satisfaction by prioritising **meal quality and restaurant service**.

## Method

1. Clean and merge reviews, hotel list and booking data; treat placeholder values as missing and impute with the mode; de-duplicate on Booking No + Hotel ID
2. Ordinal-encode ratings (0 = Unacceptable to 4 = Excellent)
3. EDA: median/mode, stacked rating distributions, Spearman correlations
4. Compute the three distance matrices on the six service features (GDM2 in R with `clusterSim`)
5. K-Medoids (PAM) for k = 2 to 8 per distance matrix; compare with Silhouette (primary) and Davies-Bouldin (secondary)
6. Profile segments (median/mode, Top-Box/Bottom-Box) and test differences (Kruskal-Wallis + epsilon-squared)

## Repository structure

```
├── notebooks/01\_ordinal\_kmedoids\_analysis.ipynb   # Python: cleaning, EDA, Gower, Podani, PAM, profiling, tests
├── src/gdm2\_distance.Rmd                          # R: GDM2 distance matrix (clusterSim)
├── results/figures/                               # charts used in the report
├── report/Research\_Report.pdf                     # full written report
├── presentation/Viva\_Presentation.pptx            # viva slides
├── data/README.md                                 # expected data structure (data not included)
└── requirements.txt
```

## Tools

Python (pandas, NumPy, SciPy, scikit-learn, `kmedoids`, matplotlib, seaborn), R (`clusterSim`)

## Data and reproducibility

The data is confidential and **not included**. See [`data/README.md`](data/README.md) for the expected columns. To reproduce with your own ordinal data: run the notebook up to the export cell, knit `src/gdm2\_distance.Rmd` to produce the GDM2 matrix, then continue the notebook.

## Limitations

Single company and unequal nationality representation; Davies-Bouldin assumes Euclidean centroids so it was only approximated and treated as secondary; GDM2 was computed in R and imported into Python.

## Future work

Link segments to nationality; compare with model-based clustering (Latent Class Analysis).

## Contact

Vestika Weerachandra | www.linkedin.com/in/vestika-weerachandra-052004187 | vestika.weerachandra@gmail.com

