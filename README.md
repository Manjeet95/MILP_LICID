
# LICID-MILP

MILP Based Differential Characteristics Search Problem for Block Cipher LICID


## Source Code

There are five files in this source code.
- Ineq_Reduction.py 
- LICID.py
- Outer_LICID_64_14.lp
- Inner_LICID_64_14.lp
- 14-round_Differential_Characteristic.txt
- LICID_in_out.py
- 12-round_Differential_Distinguisher.txt
- 11-round_Differential_Distinguisher.txt

## Generation and Reduction of Linear Inequalities

- First, Ineq_Reduction.py generates linear inequalities. Then, minimize the linear inequalities using GUROBI (to reduce the number of active S-boxes or to optimize the probability of differential characteristics).

- The command 'python Ineq_Reduction.py LICID sbox GUROBI -' gives the list of minimized linear inequalities to reduce the number of active S-boxes.

- The command 'python Ineq_Reduction.py LICID prob GUROBI -' provides the list of minimized linear inequalities to optimize the probability of differential characteristics.


## MILP model to minimize the number of active S-boxes and optimize the probability of differential characteristics

- LICID.py is used to model the MILP problem and solve it using GUROBI. Linear inequalities generated in the previous section have to be updated in this file. This file generates two modules outer and inner. The outer module minimizes the number of active S-boxes while the inner module search for differential characteristics with high probability. Both these modules are interfaced together and the user need not run these separately.

- LICID.py takes six arguments. The first argument defines block size, the second argument defines the number of rounds, the third argument defines the minimum number of active S-boxes, the fourth argument defines whether the difference of some round is fixed or not, the fifth argument defines the number of trails to find and sixth argument is used to define the solver.

- High probability differential characteristic for 14-round LICID is searched using the following command:
```bash
    python LICID.py 64 14 14 no_fix 1 GUROBI
```

- The differential characteristic is mentioned in the 14-round_Differential_Characteristic.txt file.


## Key Recovery Distinguishers

- LICID_in_out.py is used to generate 12-round and 11-round differential distinguishers as follows:
```bash
    python LICID_in_out.py 64 12 3 no_fix 1 possible GUROBI
    python LICID_in_out.py 64 11 10 no_fix 1 possible GUROBI
```
as given in 12-round_Differential_Distinguisher.txt and 11-round_Differential_Distinguisher.txt files.
