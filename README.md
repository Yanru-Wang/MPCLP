## Detailed Computational Results for the MPCLP Paper

This repository provides CSV tables with detailed computational results for the paper:

**An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem**

Yan-Ru Wang, Wei-Kun Chen, and Ivana Ljubic

The paper studies the multiple probabilistic covering location problem (MPCLP), where a fixed number of facilities are opened to maximize total covered customer demand under joint probabilistic coverage. It proposes a compact mixed-integer nonlinear formulation and an LP-based branch-and-cut algorithm strengthened by enhanced outer-approximation inequalities and lifted subadditive inequalities.

### Repository Structure

```text
data/
  summary/
    tbl_01_bin_vs_bc_summary.csv
    tbl_03_vi_four_settings_summary.csv
  detailed/
    bin_vs_bc/
      tbl_02_bin_vs_bc_*.csv
    vi_four_settings/
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

### CSV Files

#### Summary Tables

- `data/summary/tbl_01_bin_vs_bc_summary.csv`: aggregated comparison between the binary formulation (`B&C-B`) and the proposed integer formulation (`B&C-I`).
- `data/summary/tbl_03_vi_four_settings_summary.csv`: aggregated comparison among four integer-formulation settings: `vB&C-I`, `vB&C-I+E`, `vB&C-I+L`, and `B&C-I`.

#### Detailed Tables by Parameter Setting

The filename suffix encodes `(r, R, theta)`. For example, `5_20_02` means `r = 5`, `R = 20`, and `theta = 0.2`.

Binary formulation versus proposed integer formulation:

- `data/detailed/bin_vs_bc/tbl_02_bin_vs_bc_5_20_02.csv`
- `data/detailed/bin_vs_bc/tbl_02_bin_vs_bc_5_20_05.csv`
- `data/detailed/bin_vs_bc/tbl_02_bin_vs_bc_5_20_08.csv`
- `data/detailed/bin_vs_bc/tbl_02_bin_vs_bc_10_25_02.csv`
- `data/detailed/bin_vs_bc/tbl_02_bin_vs_bc_10_25_05.csv`
- `data/detailed/bin_vs_bc/tbl_02_bin_vs_bc_10_25_08.csv`

Comparison of integer-formulation settings:

- `data/detailed/vi_four_settings/tbl_04_vi_four_settings_5_20_02.csv`
- `data/detailed/vi_four_settings/tbl_04_vi_four_settings_5_20_05.csv`
- `data/detailed/vi_four_settings/tbl_04_vi_four_settings_5_20_08.csv`
- `data/detailed/vi_four_settings/tbl_04_vi_four_settings_10_25_02.csv`
- `data/detailed/vi_four_settings/tbl_04_vi_four_settings_10_25_05.csv`
- `data/detailed/vi_four_settings/tbl_04_vi_four_settings_10_25_08.csv`

### Algorithm Labels

- `B&C-B`: branch-and-cut algorithm based on the binary formulation from the state-of-the-art approach.
- `B&C-I`: proposed branch-and-cut algorithm based on the compact integer formulation, using submodular inequalities, enhanced outer-approximation inequalities, and lifted subadditive inequalities.
- `vB&C-I`: vanilla version of the integer-formulation branch-and-cut algorithm.
- `vB&C-I+E`: `vB&C-I` with enhanced outer-approximation inequalities.
- `vB&C-I+L`: `vB&C-I` with lifted subadditive inequalities.

### Column Definitions

#### Instance Parameters

- `id`: instance identifier, formatted as `instance-r-R-theta`.
- `idparam`: parameter group identifier, formatted as `r-R-theta`.
- `|V|`: number of customers and candidate facility locations.
- `K`: number of facilities to open.
- `#C1`: number of fully covered customer-location pairs.
- `#CP`: number of partially covered customer-location pairs.
- `#data`: number of instances represented by the summary row.

#### Results

- `#Sol`: number of instances solved to optimality within the 3600-second time limit.
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

The summary tables correspond to the overall performance tables in the computational-results section of the paper. The detailed tables provide the instance-level results used to build the appendix tables for each `(r, R, theta)` parameter setting.