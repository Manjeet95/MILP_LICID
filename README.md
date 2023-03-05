
# LICID-MILP

MILP Based Differential Characteristics Search Problem for Block Cipher LICID


## Source Code

There are five files in this source code.
- Ineq_Reduction.py 
- LICID.py
- Outer_LICID_64_14.lp
- Inner_LICID_64_14.lp
- 14_round_Differential_Characteristic

## Generation and Reduction of Linear Inequalities

- First, Ineq_Reduction.py generates linear inequalities. Then, minimize the linear inequalities using GUROBI (to reduce the number of active S-boxes or to optimize probability of differential characteristics).

- The command 'python Ineq_Reduction.py LICID sbox GUROBI -' gives the list of minimized linear inequalities to reduce the number of active S-boxes.

- The command 'python Ineq_Reduction.py LICID prob GUROBI -' provides the list of minimized linear inequalities to optimize probability of differential characteristics.


## MILP model to minimize number of active S-boxes and optimize probability of differential characteristics

- LICID.py is used to model the MILP problem and solve it using GUROBI. Linear inequalties generated in previous section have to be updated in this file. This file generates two modules outer and inner. The outer module minimizes number of active S-boxes while the inner module search for differential characteristics with high probability. Both these modules are interfaced together and user need not to run these separately.

- LICID.py takes six arguments. First argument defines block size, second argument defines number of rounds, third argument defines the minimum number of active S-boxes, fourth argument defines whether difference of some round is fixed or not, fifth argument defines number of trails to find and sixth argument is used to define the solver.

- High probablitiy differential characteristic for 14-round LICID is searched using following command:
```bash
    python LICID.py 64 14 14 no_fix 1 GUROBI
```

- The differential characteristic is mentioned in 14_round_Differential_Characteristic. 