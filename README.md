## Detailed Computational Results for the MPCLP Experiments

This repository provides CSV tables with detailed computational results for the maximum probabilistic covering location problem (MPCLP) experiments.

### CSV Files

The files use a two-line header, following the style of the SCFLP CSV repository. The first header line identifies the algorithm group, and the second header line gives the metric names within each group.

#### Summary Tables

- `tbl_01_bin_vs_bc_summary.csv`: aggregated comparison between the binary formulation (`B&C-B`) and the branch-and-cut integer formulation (`B&C-I`).
- `tbl_03_vi_four_settings_summary.csv`: aggregated comparison among four integer-formulation settings: `vB&C-I`, `vB&C-I+E`, `vB&C-I+L`, and `B&C-I`.

#### Detailed Tables by Parameter Setting

The suffix encodes `(r, R, theta)`. For example, `5_20_02` means `r = 5`, `R = 20`, and `theta = 0.2`.

Binary versus integer formulation:

- `tbl_02_bin_vs_bc_5_20_02.csv`
- `tbl_02_bin_vs_bc_5_20_05.csv`
- `tbl_02_bin_vs_bc_5_20_08.csv`
- `tbl_02_bin_vs_bc_10_25_02.csv`
- `tbl_02_bin_vs_bc_10_25_05.csv`
- `tbl_02_bin_vs_bc_10_25_08.csv`

Integer-formulation setting comparison:

- `tbl_04_vi_four_settings_5_20_02.csv`
- `tbl_04_vi_four_settings_5_20_05.csv`
- `tbl_04_vi_four_settings_5_20_08.csv`
- `tbl_04_vi_four_settings_10_25_02.csv`
- `tbl_04_vi_four_settings_10_25_05.csv`
- `tbl_04_vi_four_settings_10_25_08.csv`

### Column Definitions

#### Instance Parameters

- `id`: instance identifier, formatted as `instance-r-R-theta`.
- `idparam`: parameter group identifier, formatted as `r-R-theta`.
- `|V|`: number of vertices.
- `K`: coverage or facility budget parameter.
- `#C1`: number of singleton coverage sets.
- `#CP`: number of probabilistic coverage sets.
- `#data`: number of instances in a summary row.

#### Results

- `#Sol`: number of instances solved within the time limit.
- `T`: CPU time in seconds; `TL` indicates the time limit was reached.
- `N`: number of branch-and-bound nodes.
- `Gap(%)`: final optimality gap in percent.
- `RGap(%)`: root gap in percent.
- `Obj`: incumbent objective value.
- `UB`: upper bound at termination.
- `#CL`: number of local-search improvements or local cuts, depending on the setting.
- `mCL`: maximum local-search or local-cut level, depending on the setting.
- `C`: number of generated cuts.

### Algorithms

- `B&C-B`: branch-and-cut on the binary formulation.
- `vB&C-I`: vanilla branch-and-cut on the integer formulation.
- `vB&C-I+E`: integer formulation with the enhancement `E`.
- `vB&C-I+L`: integer formulation with the local-search component `L`.
- `B&C-I`: final branch-and-cut integer formulation with all enabled components.
