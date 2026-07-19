## Detailed computational results of the paper:

### An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem

### Yan-Ru Wang, Wei-Kun Chen, and Ivana Ljubic

#### [https://arxiv.org/abs/2511.17128](https://arxiv.org/abs/2511.17128)

------

This repository provides tables in CSV format with detailed results of the computational experiments conducted for the paper "An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem".


### Algorithms

The following B&C settings are compared in the computational experiments:

- **B&C-I**: The proposed B&C algorithm based on formulation (MILP) (with integer variables $\left\{y_i\right\}_{i \in \mathcal{I}}$ being used to model the co-location of facilities) in which the submodular inequalities (15a), the enhanced outer-approximation inequalities (EOA), and the lifted subadditive inequalities (LS) are separated and added to the nodes of the search tree.
- **B&C-B**: The B&C algorithm based on formulation (MILP-B) of [Alvarez-Miranda and Sinnl (2019)](https://doi.org/10.1016/j.cor.2019.04.003) (with binary variables $\left\{x_i^k\right\}_{i \in \mathcal{I}, k \in [K]}$ being used to model the co-location of facilities) in which inequalities (16c) and (16d) are separated and added to the nodes of the search tree.
- **bB&C-I**: The basic version of `B&C-I`, where both the enhanced outer-approximation inequalities (EOA) and the lifted subadditive inequalities (LS) were not implemented.
- **bB&C-I+E**: Setting `bB&C-I` with the enhanced outer-approximation inequalities (EOA).
- **bB&C-I+L**: Setting `bB&C-I` with the lifted subadditive inequalities (LS).
- **bB&C-I+E+L**: Setting `bB&C-I` with both the enhanced outer-approximation inequalities (EOA) and the lifted subadditive inequalities (LS) (which is equivalent to setting `B&C-I`).

### CSV Data Details

The repository contains the following CSV files:

- `Table3_detailed.csv`: detailed results comparing `B&C-B` and `B&C-I` on the original benchmark testset.
- `Table4_detailed.csv`: detailed results comparing `bB&C-I`, `bB&C-I+E`, `bB&C-I+L`, and `bB&C-I+E+L` on the original benchmark testset.
- `Table5_detailed.csv`: detailed results comparing `bB&C-I`, `bB&C-I+E`, `bB&C-I+L`, and `bB&C-I+E+L` on the facility-mixture second testset. This file reports low facility-probability percentages `10`, `50`, and `90` (with complementary high percentages), radius pairs `(r, R) in {(1, 20), (2, 20)}`, and `theta in {0.01, 0.1, 0.2}`.
- `T2_BnC-I_detailed.csv`: detailed B&C-I results on the facility-mixture second testset, using the same B&C-I result columns as `Table3_detailed.csv`.

The original-testset CSV files contain all `(r, R, theta)` settings in a single table. In these files, the `id` column is formatted as `instance-r-R-theta`; for example, `1-5-20-0.2` refers to instance `1` with `r = 5`, `R = 20`, and `theta = 0.2`.

The second-testset CSV files use a unique `id` formatted as `instance-r-R-theta-low-percentage` and also repeat `r`, `R`, `theta`, and `low p_i (%)` in separate columns for easier filtering. Each data row corresponds to one `(instance, r, R, theta, low p_i (%))` combination.

The CSV files use a two-line header. The first header line identifies the algorithm group, and the second header line gives the metric names within each group.

### Column Definitions

The CSV files contain the following columns:

#### Instance Parameters

- **id**: Instance identifier. In the original-testset CSV files it is formatted as `instance-r-R-theta`; in the facility-mixture CSV files, it is formatted as `instance-r-R-theta-low-percentage`, with the radius and low-probability parameters also stored in separate columns.
- **|I|**: Number of customers and candidate facility locations. 
- **K**: Number of facilities to open
- **r, R**: Inner and outer coverage radii. These are separate columns in the facility-mixture CSV files.
- **theta**: Dependency parameter that weights the correlated-coverage and independent-coverage components. This is a separate column in the facility-mixture CSV files.
- **low p_i (%)**: Percentage of facilities drawn from the low-probability range (`10`, `50`, or `90`); the high-probability percentage is its complement to 100.
- **#C1**: Number of fully covered customer-location pairs
- **#CP**: Number of partially covered customer-location pairs

#### Results

- **T**: CPU time in seconds; `TL` indicates that the time limit was reached
- **N**: Number of explored branch-and-bound nodes
- **Gap(%)**: Final optimality gap in percent
- **RGap(%)**: LP relaxation gap at the root node in percent
- **Obj**: Objective value of the optimal solution (or best incumbent)
- **UB**: Upper bound at termination
- **nCL**: Number of sites at which facilities are co-located, reported in `Table3_detailed.csv` and `T2_BnC-I_detailed.csv`
- **mCL**: Maximum number of facilities opened at a single site, reported in `Table3_detailed.csv` and `T2_BnC-I_detailed.csv`
- **#Cut**: Total number of generated cuts
- **#MaxSM**: Number of generated submodular cuts for max terms
- **#ProdSM**: Number of generated submodular cuts for product terms, reported for the binary setting
- **#OA**: Number of generated outer-approximation cuts for product terms
- **#EOA**: Number of generated enhanced outer-approximation cuts for product terms
- **#LS**: Number of generated lifted subadditive cuts for product terms

### Computational Setting

The experiments use 240 MPCLP benchmark instances from the literature. These instances are constructed from 40 K-median instances in the OR-Library, with uniform customer demands and identical numbers of customers and candidate facility locations.

The branch-and-cut algorithm was implemented in Julia 1.7.3 with CPLEX 20.1.0. The reported experiments use a 3600-second time limit and a 0% relative MIP gap tolerance. The computations were run on Intel Xeon Gold 6140 CPU @ 2.30GHz machines.

The published CSVs are regenerated from the active `2026-07-15_yry` baseline:
1,200 original-testset records and 4,560 facility-mixture T2 records. The
summaries are rebuilt from their declared remote raw-log paths, then validated
and rendered through OR-Stat-Kit before the detailed CSV export.
