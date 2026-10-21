# Radiative evolutionary game: data

Data for **Global convergence and transient temperature limits in a radiative evolutionary game of emission strategies**, by Himanshu Jain and Purnedu Mishra.

**[Download the complete data archive](https://github.com/hjain-nitrr/Eco-evolutionary/blob/main/Eco-evolutionary_data_only.zip).** Folder paths below refer to files inside the ZIP. The data dictionary, citation metadata, manifest and checksums are also available directly in the repository. `manifest.json` inventories the archive contents.

This deposit contains the **author-processed annual dataset and model-generated numerical data**, with provenance, baseline parameters and numerical validation records. Public NOAA/NASA source data are linked below rather than redistributed. **No figures, figure-data exports, MATLAB files or source code are uploaded.** The MATLAB analysis and figure-generation code is available from the corresponding author on request: Purnedu Mishra, pmishra@iiitm.ac.in.

## Public observational sources

| Source | Official data | Documentation |
|---|---|---|
| NOAA Global Monitoring Laboratory, Annual Greenhouse Gas Index (AGGI) | [AGGI_Table.csv](https://gml.noaa.gov/aggi/AGGI_Table.csv) | [NOAA AGGI](https://gml.noaa.gov/aggi/aggi.html) |
| NASA GISS, GISTEMP v4 global Land-Ocean Temperature Index | [Global land-ocean CSV](https://data.giss.nasa.gov/gistemp/tabledata_v4/GLB.Ts%2BdSST.csv) | [GISTEMP v4](https://data.giss.nasa.gov/gistemp/data_v4.html) |

The analysis uses the common complete period **1979–2024**. Temperature anomalies use the NASA 1951–1980 reference period. The processed annual series is supplied in `data/observations_1979_2024.csv`; raw public-source CSVs are not included. Current official files can be revised and need not match the historical snapshots used in the analysis.

## Data in the archive

| Folder/file | Contents |
|---|---|
| `data/observations_1979_2024.csv` | Aligned annual forcing, AGGI and temperature-anomaly data, 46 rows |
| `data/provenance.json` | Original source/retrieval record and historical snapshot hashes |
| `tables/uncertainty_ensemble.csv` | 4000 sampled parameter sets and equilibrium classifications |
| `tables/local_sensitivity_derivatives.csv` | Local derivatives for 1527 retained mixed-equilibrium cases |
| `tables/conditional_prcc.csv` | Conditional rank correlations and descriptive bootstrap intervals |
| `tables/transient_ceiling_grid.csv` | 729 rate/initial-share combinations, finite-horizon peaks and certificate margins |
| `tables/cost_comparison_7a.csv`, `tables/cost_comparison_7b.csv` | Numerical equilibrium data under two cost conventions, 601 incentives per reference scenario |
| `tables/heat_capacity_recovery.csv` | 301 heat-capacity values and minimum local recovery times |
| `tables/results.json` | Aggregate numerical results and parameter values |
| `tables/*checks.json`, `tables/validation.json` | Original finite numerical check records |
| `metadata/` | Baseline parameters, source links, package metadata and packaging checks |
| `DATA_DICTIONARY.md` | Units, column definitions, regime codes and sampling details |
| `CITATION.cff` | Dataset citation metadata |
| `manifest.json`, `SHA256SUMS` | Archive inventory and SHA-256 checksums |

The CSV and JSON data can be read without MATLAB. The original computations used MATLAB R2024a Update 8. The seven numerical CSV tables and original JSON result/check records were copied without changing their values. No model integrations, bootstrap resampling or observational retrieval were rerun for this deposit.

## Provenance

The frozen inputs were prepared on 19 October 2026. NOAA's source CSV was downloaded directly. The NASA numerical snapshot was obtained through Exa from the official NASA CSV after direct download attempts timed out; it was not a byte-for-byte original-source download. This limitation is preserved in `data/provenance.json`. That original record includes hashes of raw snapshots retained by the authors as well as the processed file; a listed hash does not mean that every historical source file is redistributed here. The manifest lists exactly what this deposit contains.

## Interpretation

The observations provide a radiative-scale comparison, not a fit of behavioral parameters or a historical temperature prediction. The 288 K benchmark is an explicit convention. Ensemble frequencies depend on the chosen parameter design. PRCCs and their intervals are conditional on retained mixed cases and do not estimate future societal probabilities. The ceiling grid covers 600 years; numerical compliance outside the analytical certificate is not an all-time guarantee. Numerical check records apply to their stated finite cases; universal results rest on the manuscript's proofs.

## Version, citation and code

Data version: **2026-10-21-data-v1**. Frozen analysis source: **2026-10-19-r5-AMC-academic-prose-and-assumption-figures**. Cite the official NOAA/NASA sources for their observations and this repository for the processed and model-generated datasets. Citation metadata is in `CITATION.cff`.

**The MATLAB analysis and figure-generation code is available from the corresponding author on request.**
