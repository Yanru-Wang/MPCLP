## Detailed computational results of the paper:

### An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem

### Yan-Ru Wang, Wei-Kun Chen, and Ivana Ljubic

#### [https://arxiv.org/abs/2511.17128](https://arxiv.org/abs/2511.17128)

------

This repository provides tables in CSV format with detailed results of the computational experiments conducted for the paper "An efficient branch-and-cut algorithm for the multiple probabilistic covering location problem".


### Algorithms

The following B&C settings are compared in the computational experiments:

- **B&C-B**: Re-implemented Branch-and-Cut algorithm based on the binary formulation of the state-of-the-art approach, where binary variables are used to model the co-location of facilities
- **B&C-I**: Proposed Branch-and-Cut algorithm based on the compact integer formulation, where integer variables are used to model the co-location of facilities; submodular inequalities, enhanced outer-approximation inequalities, and lifted subadditive inequalities are separated and added to the nodes of the search tree
- **vB&C-I**: Basic version of `B&C-I`, where the enhanced outer-approximation inequalities and lifted subadditive inequalities are not implemented
- **vB&C-I+E**: `vB&C-I` with enhanced outer-approximation inequalities
- **vB&C-I+L**: `vB&C-I` with lifted subadditive inequalities
- **vB&C-I+E+L**: `vB&C-I` with both enhanced outer-approximation inequalities and lifted subadditive inequalities; this setting is equivalent to `B&C-I`

### CSV Data Details

The repository contains the following CSV files:

- `bin_vs_bc.csv`: detailed results comparing `B&C-B` and `B&C-I`
- `vi_four_settings.csv`: detailed results comparing `vB&C-I`, `vB&C-I+E`, `vB&C-I+L`, and `vB&C-I+E+L`

Each CSV file contains all `(r, R, theta)` settings in a single table. The `id` column is formatted as `instance-r-R-theta`; for example, `1-5-20-0.2` refers to instance `1` with `r = 5`, `R = 20`, and `theta = 0.2`.

The CSV files use a two-line header. The first header line identifies the algorithm group, and the second header line gives the metric names within each group.

### Column Definitions

The CSV files contain the following columns:

#### Instance Parameters

- **id**: Instance identifier, formatted as `instance-r-R-theta`
- **|V|**: Number of customers and candidate facility locations
- **K**: Number of facilities to open
- **#C1**: Number of fully covered customer-location pairs
- **#CP**: Number of partially covered customer-location pairs

#### Results

- **T**: CPU time in seconds; `TL` indicates that the time limit was reached
- **N**: Number of explored branch-and-bound nodes
- **Gap(%)**: Final optimality gap in percent
- **RGap(%)**: LP relaxation gap at the root node in percent
- **Obj**: Incumbent objective value
- **UB**: Upper bound at termination
- **#CL**: Number of generated local-search/cut components recorded by the final setting
- **mCL**: Maximum local-search/cut level recorded by the final setting
- **#Cut**: Total number of generated cuts
- **#MaxSM**: Number of generated submodular cuts for max terms
- **#ProdSM**: Number of generated submodular cuts for product terms, reported for the binary setting
- **#OA**: Number of generated outer-approximation cuts for product terms
- **#EOA**: Number of generated enhanced outer-approximation cuts for product terms
- **#LS**: Number of generated lifted subadditive cuts for product terms

### Computational Setting

The experiments use 240 MPCLP benchmark instances from the literature. These instances are constructed from 40 K-median instances in the OR-Library, with uniform customer demands and identical numbers of customers and candidate facility locations.

The branch-and-cut algorithm was implemented in Julia 1.7.3 with CPLEX 20.1.0. The reported experiments use a 3600-second time limit and a 0% relative MIP gap tolerance. The computations were run on Intel Xeon Gold 6140 CPU @ 2.30GHz machines.
