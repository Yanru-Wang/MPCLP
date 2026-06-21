## Detailed computational results of the paper:

### An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem

### Yan-Ru Wang, Wei-Kun Chen, and Ivana Ljubic

#### [https://arxiv.org/abs/2511.17128](https://arxiv.org/abs/2511.17128)

------

This repository provides tables in CSV format with detailed results of the computational experiments conducted for the paper "An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem".


### Algorithms

The following B&C settings are compared in the computational experiments:

- **B&C-I**: The proposed B&C algorithm based on formulation (MILP) (with integer variables $\{y_i\}_{i \in \mathcal{I}}$ being used to model the co-location of facilities) in which the submodular inequalities (15a), the enhanced outer-approximation inequalities (EOA), and the lifted subadditive inequalities (LS) are separated and added to the nodes of the search tree.
- **B&C-B**: The B&C algorithm based on formulation (MILP-B) of [Alvarez-Miranda and Sinnl (2019)](https://doi.org/10.1016/j.cor.2019.04.003) (with binary variables $\{x_i^k\}_{i \in \mathcal{I}, k \in [K]}$ being used to model the co-location of facilities) in which inequalities (16c) and (16d) are separated and added to the nodes of the search tree.
- **bB&C-I**: The basic version of `B&C-I`, where both the enhanced outer-approximation inequalities (EOA) and the lifted subadditive inequalities (LS) were not implemented.
- **bB&C-I+E**: Setting `bB&C-I` with the enhanced outer-approximation inequalities (EOA).
- **bB&C-I+L**: Setting `bB&C-I` with the lifted subadditive inequalities (LS).
- **bB&C-I+E+L**: Setting `bB&C-I` with both the enhanced outer-approximation inequalities (EOA) and the lifted subadditive inequalities (LS) (which is equivalent to setting `B&C-I`).

### CSV Data Details

The repository contains the following CSV files:

- `bin_vs_bc.csv`: detailed results comparing `B&C-B` and `B&C-I` on the original benchmark testset.
- `vi_four_settings.csv`: detailed results comparing `bB&C-I`, `bB&C-I+E`, `bB&C-I+L`, and `bB&C-I+E+L` on the original benchmark testset.
- `vi_four_settings_testset2_ps_selected.csv`: detailed results comparing `bB&C-I`, `bB&C-I+E`, `bB&C-I+L`, and `bB&C-I+E+L` on the second testset with stepwise coverage probabilities. This file reports the selected values `p_s in {0.1, 0.2, 0.5}` and radius pairs `(r, R) in {(1, 20), (2, 20)}`.

The original-testset CSV files contain all `(r, R, theta)` settings in a single table. In these files, the `id` column is formatted as `instance-r-R-theta`; for example, `1-5-20-0.2` refers to instance `1` with `r = 5`, `R = 20`, and `theta = 0.2`.

The second-testset CSV file uses a unique `id` formatted as `instance-r-R-theta-p_s` and also repeats `r`, `R`, `theta`, and `p_s` in separate columns for easier filtering. Each data row corresponds to one `(instance, r, R, theta, p_s)` combination.

The CSV files use a two-line header. The first header line identifies the algorithm group, and the second header line gives the metric names within each group.

### Column Definitions

The CSV files contain the following columns:

#### Instance Parameters

- **id**: Instance identifier. In the original-testset CSV files it is formatted as `instance-r-R-theta`; in `vi_four_settings_testset2_ps_selected.csv`, it is formatted as `instance-r-R-theta-p_s`, with the radius and probability parameters also stored in separate columns.
- **|I|**: Number of customers and candidate facility locations. 
- **K**: Number of facilities to open
- **r, R**: Inner and outer coverage radii. These are separate columns in `vi_four_settings_testset2_ps_selected.csv`.
- **theta**: Demand coverage threshold. This is a separate column in `vi_four_settings_testset2_ps_selected.csv`.
- **p_s**: Intermediate stepwise coverage probability, reported in `vi_four_settings_testset2_ps_selected.csv`.
- **#C1**: Number of fully covered customer-location pairs
- **#CP**: Number of partially covered customer-location pairs

#### Results

- **T**: CPU time in seconds; `TL` indicates that the time limit was reached
- **N**: Number of explored branch-and-bound nodes
- **Gap(%)**: Final optimality gap in percent
- **RGap(%)**: LP relaxation gap at the root node in percent
- **Obj**: Objective value of the optimal solution (or best incumbent)
- **UB**: Upper bound at termination
- **#CL**: Number of generated local-search/cut components, reported in `bin_vs_bc.csv`
- **mCL**: Maximum local-search/cut level, reported in `bin_vs_bc.csv`
- **#Cut**: Total number of generated cuts
- **#MaxSM**: Number of generated submodular cuts for max terms
- **#ProdSM**: Number of generated submodular cuts for product terms, reported for the binary setting
- **#OA**: Number of generated outer-approximation cuts for product terms
- **#EOA**: Number of generated enhanced outer-approximation cuts for product terms
- **#LS**: Number of generated lifted subadditive cuts for product terms

### Computational Setting

The experiments use 240 MPCLP benchmark instances from the literature. These instances are constructed from 40 K-median instances in the OR-Library, with uniform customer demands and identical numbers of customers and candidate facility locations.

The branch-and-cut algorithm was implemented in Julia 1.7.3 with CPLEX 20.1.0. The reported experiments use a 3600-second time limit and a 0% relative MIP gap tolerance. The computations were run on Intel Xeon Gold 6140 CPU @ 2.30GHz machines.
