## Detailed Computational Results for the MPCLP Paper

This repository provides detailed computational results for the paper:

**An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem**

Yan-Ru Wang, Wei-Kun Chen, and Ivana Ljubic

The paper studies the multiple probabilistic covering location problem (MPCLP), where a fixed number of facilities are opened to maximize total covered customer demand under joint probabilistic coverage. It proposes a compact mixed-integer nonlinear formulation and an LP-based branch-and-cut algorithm strengthened by enhanced outer-approximation inequalities and lifted subadditive inequalities.

### Repository Structure

```text
comparison_with_state_of_the_art_approach/
  tbl_02_bin_vs_bc_*.csv
performance_effect_of_enhanced_outer_approximation_and_lifted_subadditive_inequalities/
  tbl_04_vi_four_settings_*.csv
```

The CSV files use a two-line header, following the companion CSV style used for related computational-result repositories. The first header line identifies the algorithm group; the second header line gives the metric names within each group.

### Computational Setting

The experiments in the paper use 240 MPCLP benchmark instances from the literature. These instances are constructed from 40 K-median instances in the OR-Library, with uniform customer demands and identical numbers of customers and candidate facility locations.

The instance parameters are:

- `|V|`: number of customers and candidate facility locations, up to 900.
- `K`: number of facilities to open, ranging from 5 to 200.
- `(r, R)`: minimum and maximum coverage distances, selected from `(5, 20)` and `(10, 25)`.
- `theta`: reliability parameter, selected from `0.2`, `0.5`, and `0.8`.

The branch-and-cut algorithm was implemented in Julia 1.7.3 with CPLEX 20.1.0. The reported experiments use a 3600-second time limit and a 0% relative MIP gap tolerance. The computations were run on Intel Xeon Gold 6140 CPU @ 2.30GHz machines.

### Result Tables

The filename suffix encodes `(r, R, theta)`. For example, `5_20_02` means `r = 5`, `R = 20`, and `theta = 0.2`.

#### Comparison with the State-of-the-Art Approach

These files correspond to the appendix tables titled "Performance comparison of settings `B&C-B` and `B&C-I`" for each `(r, R, theta)` setting.

- `comparison_with_state_of_the_art_approach/tbl_02_bin_vs_bc_5_20_02.csv`
- `comparison_with_state_of_the_art_approach/tbl_02_bin_vs_bc_5_20_05.csv`
- `comparison_with_state_of_the_art_approach/tbl_02_bin_vs_bc_5_20_08.csv`
- `comparison_with_state_of_the_art_approach/tbl_02_bin_vs_bc_10_25_02.csv`
- `comparison_with_state_of_the_art_approach/tbl_02_bin_vs_bc_10_25_05.csv`
- `comparison_with_state_of_the_art_approach/tbl_02_bin_vs_bc_10_25_08.csv`

#### Performance Effect of the Enhanced Outer-Approximation and Lifted Subadditive Inequalities

These files correspond to the appendix tables titled "Performance comparison of settings `vB&C-I`, `vB&C-I+E`, `vB&C-I+L`, and `B&C-I`" for each `(r, R, theta)` setting.

- `performance_effect_of_enhanced_outer_approximation_and_lifted_subadditive_inequalities/tbl_04_vi_four_settings_5_20_02.csv`
- `performance_effect_of_enhanced_outer_approximation_and_lifted_subadditive_inequalities/tbl_04_vi_four_settings_5_20_05.csv`
- `performance_effect_of_enhanced_outer_approximation_and_lifted_subadditive_inequalities/tbl_04_vi_four_settings_5_20_08.csv`
- `performance_effect_of_enhanced_outer_approximation_and_lifted_subadditive_inequalities/tbl_04_vi_four_settings_10_25_02.csv`
- `performance_effect_of_enhanced_outer_approximation_and_lifted_subadditive_inequalities/tbl_04_vi_four_settings_10_25_05.csv`
- `performance_effect_of_enhanced_outer_approximation_and_lifted_subadditive_inequalities/tbl_04_vi_four_settings_10_25_08.csv`

### Algorithm Labels

- `B&C-B`: branch-and-cut algorithm based on the binary formulation from the state-of-the-art approach.
- `B&C-I`: proposed branch-and-cut algorithm based on the compact integer formulation, using submodular inequalities, enhanced outer-approximation inequalities, and lifted subadditive inequalities.
- `vB&C-I`: vanilla version of the integer-formulation branch-and-cut algorithm.
- `vB&C-I+E`: `vB&C-I` with enhanced outer-approximation inequalities.
- `vB&C-I+L`: `vB&C-I` with lifted subadditive inequalities.

### Column Definitions

#### Instance Parameters

- `id`: instance identifier, formatted as `instance-r-R-theta`.
- `|V|`: number of customers and candidate facility locations.
- `K`: number of facilities to open.
- `#C1`: number of fully covered customer-location pairs.
- `#CP`: number of partially covered customer-location pairs.

#### Results

- `T`: CPU time in seconds; `TL` indicates that the time limit was reached.
- `N`: number of branch-and-bound nodes.
- `Gap(%)`: final optimality gap in percent.
- `RGap(%)`: LP relaxation gap at the root node in percent.
- `Obj`: incumbent objective value.
- `UB`: upper bound at termination.
- `#CL`: number of generated local-search/cut components recorded by the final setting.
- `mCL`: maximum local-search/cut level recorded by the final setting.
- `C`: total number of generated cuts.

### Notes

The detailed CSV files provide the instance-level results used to build the appendix tables for each `(r, R, theta)` parameter setting. Overall summary tables are intentionally not included in this repository.
