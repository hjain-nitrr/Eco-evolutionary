# Data dictionary

## Observational files

`data/noaa_aggi_raw.csv` preserves the NOAA source bytes. Its two columns named `Total` have different meanings: the first is total long-lived greenhouse-gas effective radiative forcing in W m^-2; the second is CO2-equivalent concentration, not forcing. Use the processed files to avoid ambiguous duplicate column names.

`data/noaa_aggi_1979_2024.csv` has 46 annual rows:

| Column | Meaning / units |
|---|---|
| `Year` | Calendar year, 1979–2024 |
| `CO2_Wm2` | CO2 effective radiative forcing, W m^-2 |
| `Total_Wm2` | Total long-lived greenhouse-gas effective radiative forcing, W m^-2 |
| `AGGI` | Annual Greenhouse Gas Index, dimensionless; 1990 = 1 |

`data/nasa_gistemp_v4_snapshot.csv` preserves the frozen numerical-text snapshot. The first line is a title, the second a header. Monthly columns and `J-D` (annual), `D-N`, `DJF`, `MAM`, `JJA`, `SON` report temperature anomalies relative to 1951–1980. Temperature-anomaly increments in degrees Celsius equal increments in kelvin. Source missing-value markers must not be treated as zero. The analysis uses `J-D` only for 1979–2024; the snapshot also contains years outside that analysis window.

`data/observations_1979_2024.csv` aligns the annual records:

| Column | Meaning / units |
|---|---|
| `Year` | Calendar year |
| `CO2_ERF_Wm2` | NOAA CO2 effective radiative forcing, W m^-2 |
| `LLGHG_ERF_Wm2` | NOAA total long-lived greenhouse-gas effective radiative forcing, W m^-2 |
| `AGGI` | Dimensionless index, 1990 = 1 |
| `GISTEMP_anomaly_1951_1980_K` | NASA annual global land-ocean temperature anomaly, K |

`data/provenance.json` records retrieval routes, URLs, analysis years, benchmark conventions and hashes. The observational files do not supply newly constructed confidence intervals.

## Model parameters and sampling

The model state is temperature `T` in K and high-emission strategy share `x` in [0,1]. Time is in years in the numerical tables. `metadata/baseline_parameters.json` records the exact baseline values. `sigma` is in W m^-2 K^-4, `R` in W m^-2, `C` in J m^-2 K^-1; `epsilon_LE`, `epsilon_HE` and `E` are dimensionless; `r`, `T0`, `T1`, `Tstar`, `Tlim`, `Tfold` are in K; `D` is in K^-2; `k` is in m^2 W^-1; `nu` is in yr^-1. `K=k*sigma*E/D`, with units K^-2. `k0`, `k1`, `kstar` and `kfold` have the same units as `k`; `K0` and `K1` have the same units as `K`.

The five-coordinate design uses stratified randomized marginal coordinates: k in [0.4 baseline k0, 1.4 baseline k1], D in [0.01,0.04], E in [0.9 baseline E,1.1 baseline E], r in [285,287] K, and log10(nu/(1 yr^-1)) in [-1,1]. Local regime thresholds are recalculated for each draw. Seeds are 271829 (2000 draws), 271830 (4000 draws) and 314159 (300 conditional bootstrap resamples), using MATLAB `twister`. Validation uses seed 104729.

## Numerical tables

### `tables/uncertainty_ensemble.csv`

4000 draws. `k`, `D`, `E`, `r_K` and `nu_per_year` are sampled inputs with the units above. `Tstar_K` and `xstar` describe the stable interior mixed equilibrium and are `NaN` when no such equilibrium is retained. `regime_code` is **1 = LE boundary, 2 = mixed, 3 = HE boundary**. Counts are 1359, 1527 and 1114 respectively. `NaN` means not applicable, not zero.

### `tables/local_sensitivity_derivatives.csv`

1527 retained mixed-equilibrium cases in the order they occur in the ensemble. `Tstar_K`, `xstar` are equilibrium coordinates. `dT_dk`, `dT_dD`, `dT_dr`, `dT_dE` are local temperature derivatives; `dx_dk`, `dx_dD`, `dx_dr`, `dx_dE` are local share derivatives. Each derivative has units of its numerator divided by the corresponding parameter's units. Other parameters are held fixed. These are derivatives, not PRCCs; in particular, `dx_dE` may have either sign.

### `tables/conditional_prcc.csv`

Five rows, one per parameter (`k`, `D`, `E`, `r`, `nu`). `PRCC_T` and `PRCC_x` are dimensionless partial rank correlation coefficients conditional on the 1527 retained mixed cases. `T_lower`, `T_upper`, `x_lower`, `x_upper` are descriptive 95% percentile bootstrap intervals from 300 conditional resamples. They are not temperature or strategy-share measurement intervals.

### `tables/transient_ceiling_grid.csv`

729 initial-state/rate combinations (27 × 27). `nu_per_year` is the social update rate; `initial_HE_share` is x(0). Initial temperature is fixed at the baseline mixed temperature. `peak_exceedance_K` is the largest sampled/solver-located temperature over 600 years minus the prescribed ceiling; positive values indicate exceedance. `Lyapunov_barrier_margin` is V_L minus V(T(0),x(0)); positive values satisfy the sufficient certificate. The grid is not a complete viability boundary. Peaks include solver-located downward crossings of the temperature rate, endpoints and a 0.25-year reporting grid.

### `tables/cost_comparison_7a.csv` and `cost_comparison_7b.csv`

601 incentive values per scenario. `k_m2_per_W` is the incentive; `k_over_baseline_k1` divides it by the principal baseline k1, not a threshold recomputed for the new reference. The three `two_sided_stable_*` columns contain normalized equilibrium temperature (T*-T0)/(T1-T0) on the LE, mixed and HE branches; `NaN` denotes an absent stable branch. `one_sided_stable_temperature_normalized` is the attracting temperature for the one-sided cost. Panel 7a uses r=286 K; panel 7b uses r=T0+0.35(T1-T0). These normalized temperatures are dimensionless.

### `tables/heat_capacity_recovery.csv`

301 heat capacities. `C_J_per_m2_K` is the assumed heat capacity. `minimum_local_time_years` is C*T*/(2*R), converted from seconds to years using `seconds_per_year`, at fixed equilibrium and other baseline parameters. These are model quantities, not heat-capacity estimates from observations.

## Aggregate results and validation

`tables/results.json` and `tables/results.mat` contain aggregate physical, recovery, ceiling, uncertainty and baseline-parameter results. `tables/validation.json`, `tables/cost_convention_checks.json` and `tables/assumption_figure_checks.json` retain the original finite numerical check results. `metadata/computation_contract.json`, `metadata/bounded_run_manifest.json` and `metadata/cost_check_provenance.json` document the declared ranges, software, seeds, historical execution and original artifact hashes. Their source-code references describe withheld files.

## Figure-data schema

`figure_data/index.json` lists the 21 panel stems, number of axes and number of numeric graphic objects. Each `<panel>.json` has `panel`, `source_figure`, export method, software and `axes`. Each axis records its title, coordinate labels, scales, limits, color limits and `objects`. Labels are retained as saved; some are cell arrays of strings. Each object records its graphics type, display name and available numeric properties:

- `XData`, `YData`, `ZData`: coordinates; vectors or matrices as appropriate.
- `CData`, `FaceVertexCData`: scalar/category/color arrays as stored by MATLAB.
- `UData`, `VData`, `WData`: vector-field components.
- Error-bar delta properties: positive/negative coordinate uncertainties as plotted.
- `ContourMatrix`, `LevelList`: MATLAB contour representation and levels.
- `Value`: constant reference-line coordinate; its orientation is inferred from the labeled panel/context.
- `Values`, `BinEdges`, `BaseValue`: bar/histogram properties when present.

JSON `null` represents nonfinite numeric values. The `nonfinite` object records NaN and signed-infinity positions using **one-based MATLAB column-major linear indices**. `<panel>.mat` preserves the same `figureData` structure with native numeric arrays and nonfinite values. Scientific traces may coexist with legend proxies, reference curves and graphics children; object order is not a scientific ordering and duplicate rendered components must not be treated as additional independent observations.

| Panels | Content |
|---|---|
| 1a, 1b, 1c | Observations and fixed-temperature radiative-scale comparison |
| 2a, 2b | Feasible equilibrium branches for two reference positions |
| 3a | Reference-position/selection atlas: CData codes 1=LE, 2=mixed, 3=HE, 4=LE+mixed, 5=LE+HE |
| 3b, 3c | Phase-plane trajectories, nullcline and vector-field data |
| 4a, 4b | Local recovery spectrum, exchanges and rate ceiling |
| 4c, 4d | Temperature and strategy transients |
| 5a | Equilibrium compliance atlas: CData 1=LE compliant, 2=mixed compliant, 3=mixed exceeds, 4=HE exceeds |
| 5b, 5c | Finite-horizon exceedance and Lyapunov-certificate data |
| 6a, 6b, 6c | Regime fractions and conditional PRCCs |
| 7a, 7b | Cost-convention comparisons |
| 8a | Heat capacity and fastest local recovery time |

`metadata/figure_source_hashes.json` identifies the original saved figures used for extraction. No simulations were rerun to make these exports. Shape-preserving graphics-property data are supplied for transparency; use the manuscript's definitions and the tabular data for statistical analysis.
