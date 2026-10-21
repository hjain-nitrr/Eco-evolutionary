# Radiative evolutionary game: data

Data accompanying **Global convergence and transient temperature limits in a radiative evolutionary game of emission strategies**, by Himanshu Jain and Purnedu Mishra.

This repository supplies the frozen observational inputs, processed annual observations, sampled model parameters, numerical results, validation records and numerical data extracted from all 21 saved figure panels. **MATLAB source code is available from the corresponding author on request**: Purnedu Mishra, pmishra@iiitm.ac.in. The code is not included in this repository.

## Contents

| Folder/file | Contents |
|---|---|
| `data/` | Frozen NOAA AGGI and NASA GISTEMP v4 snapshots, the processed 1979–2024 series and original retrieval provenance |
| `tables/` | All seven saved CSV numerical tables; aggregate results in JSON and MAT format; original numerical validation/check records |
| `figure_data/` | Numerical graphics properties for panels 1a–8a in JSON and MAT format, with `index.json`; 21 panels across eight figure groups |
| `metadata/` | Baseline parameters, data metadata, original computation/run records and hashes identifying the source FIG files |
| `DATA_DICTIONARY.md` | Column definitions, units, regime codes and interpretation of the figure-data exports |
| `CITATION.cff` | Citation metadata for this data repository |
| `manifest.json`, `SHA256SUMS` | File inventory and SHA-256 checksums |

Use `data/observations_1979_2024.csv` for the aligned annual observational series. Use `tables/uncertainty_ensemble.csv` for the 4000-draw model ensemble and `tables/results.json` for the reported numerical summaries. The original computations used MATLAB R2024a Update 8. CSV and JSON files can be read without MATLAB; MAT files contain data, not executable scripts.

## Observational sources and provenance

- **NOAA Global Monitoring Laboratory, Annual Greenhouse Gas Index (AGGI)**: [documentation](https://gml.noaa.gov/aggi/aggi.html), [source CSV](https://gml.noaa.gov/aggi/AGGI_Table.csv). The frozen source is the Fall 2025 update recorded in `data/provenance.json`.
- **NASA GISS, GISTEMP v4 global Land-Ocean Temperature Index**: [documentation](https://data.giss.nasa.gov/gistemp/data_v4.html), [source CSV](https://data.giss.nasa.gov/gistemp/tabledata_v4/GLB.Ts%2BdSST.csv). Anomalies use the 1951–1980 reference period.

The observational analysis uses the common complete period **1979–2024**. NOAA's CSV was downloaded directly. The frozen NASA file contains numerical text obtained through Exa from the official NASA CSV after direct download attempts timed out; it is not an authenticated byte-for-byte download of the official CSV. This limitation and the exact hashes of the files used are preserved in `data/provenance.json`. A file hash identifies the local snapshot; it does not independently authenticate its source. No new observation retrieval was performed for this data release.

## Numerical scope

The data document an illustrative radiative scale and a declared model scenario. They do not calibrate the behavioral parameters or constitute a historical climate prediction. The 288 K benchmark is a stated convention, not an estimate of absolute observed global temperature. Attractor frequencies depend on the chosen parameter design. PRCCs and bootstrap intervals are conditional on the retained mixed-equilibrium cases and are not estimates of future societal probabilities.

The temperature-ceiling grid covers a finite 600-year horizon. Positive Lyapunov barrier margins identify the analytical sufficient certificate at the sampled initial states; finite-horizon compliance outside that set is not an all-time guarantee. Numerical validation records describe the finite checks actually run. Universal claims rest on the manuscript's proofs.

## Figure data

The `figure_data` files were extracted from the existing saved MATLAB figures; simulations were not rerun. Files retain the original panel stems (`1a`, `1b`, …, `8a`). They record plotted coordinates, image/surface arrays, contour data, error bars, reference-line values and axis metadata. See the dictionary for the schema and limitations. These are numerical data exports, not substitutes for the withheld plotting/analysis code. Source figure hashes identify precisely which assets were read.

## Version and availability

Data package: **2026-10-21-data-v1**. Frozen analysis source: **2026-10-19-r5-AMC-academic-prose-and-assumption-figures**. The subsequent language revisions do not generate a new observational dataset in this package. Original JSON run records retain historical paths and command descriptions for provenance; references to MATLAB files do not mean those files are included here.

The MATLAB analysis and figure-generation code is available from the corresponding author on request. Cite the original NOAA/NASA sources when using those observations, and cite this repository for the processed and model-generated data. Repository citation metadata is supplied in `CITATION.cff`. No DOI or journal acceptance is claimed.
