# Supplementary

## Solver

### Introduction

ArithPartition is a dynamic parallel framework with arithmetic variable-level partitioning for SMT solving in arithmetic theories, which is proposed in the paper "Distributed SMT Solving Based on Dynamic Variable-level Partitioning."

[![pFmSkTI.png](https://s11.ax1x.com/2024/01/24/pFmSkTI.png)](https://imgse.com/i/pFmSkTI)


### Requirements

x86_64， Linux with GLIBC version >= 2.29


### Usage

`solver/ArithPartiton` is an executable binary file.

Here is an example:

```bash
cd solver

./ArithPartition \
--file ../test-instances/lia-unsat-17.8.smt2 \
--output-dir  ../test-instances/test-output-dir/ \
--partitioner  ./partitioner/partitioner \
--solver ./base-solvers/cvc5-1.0.8 \
--max-running-tasks 8 \
--time-limit 1200
```

If nothing unexpected happens, it will output as follows:

The first line is the solution result, and the second is the solving time.

```
unsat
17.75242280960083
```

The following are the explanations for each parameter:


| Parameters          | Explanation                                                  |
| ------------------- | ------------------------------------------------------------ |
| --file              | The path to SMT instance, ending with .smt2.                 |
| --output-dir        | The path to the output folder for temporary and result files. |
| --partitioner       | The path of the partitioner, which is located in this location: solver/partitioner/partitioner. |
| --solver            | The path to the base solver. Three SMT solvers compared in the paper are placed in the solver/base-solvers directory. You can also use any other solver with a standard input and output format. |
| --max-running-tasks | The maximum number of working processes.                     |
| --time-limit        | Time limit returns 'unknown' if it exceeds the limit.       |

## Experiment Results

The dir `experiment-results` contains all the experimental results mentioned in the paper "Distributed SMT Solving Based on Dynamic Variable-level Partitioning."

There are four theories in this dir, and each dir has a sum-up file `results-sumup.txt` in a table format like this:

```
╒═════════════════════════╤═══════╤═════════╤══════════╤══════════╤═════════╕
│ solver                  │   sat │   unsat │   solved │   failed │   PAR-2 │
╞═════════════════════════╪═══════╪═════════╪══════════╪══════════╪═════════╡
│ cvc5-1.0.8-p1           │  5485 │    5811 │    11296 │      838 │ 2100561 │
├─────────────────────────┼───────┼─────────┼──────────┼──────────┼─────────┤
│ cvc5-1.0.8-p8           │  5559 │    5798 │    11357 │      777 │ 1948280 │
├─────────────────────────┼───────┼─────────┼──────────┼──────────┼─────────┤
│ cvc5-1.0.8-p16          │  5575 │    5796 │    11371 │      763 │ 1920929 │
├─────────────────────────┼───────┼─────────┼──────────┼──────────┼─────────┤
│ ArithPartition-cvc5-p8  │  5709 │    5864 │    11573 │      561 │ 1425236 │
├─────────────────────────┼───────┼─────────┼──────────┼──────────┼─────────┤
│ ArithPartition-cvc5-p16 │  5731 │    5864 │    11595 │      539 │ 1372485 │
├─────────────────────────┼───────┼─────────┼──────────┼──────────┼─────────┤
│ z3-4.12.1-p1            │  5626 │    5375 │    11001 │     1133 │ 2770153 │
├─────────────────────────┼───────┼─────────┼──────────┼──────────┼─────────┤
│ ArithPartition-z3-p8    │  5744 │    5686 │    11430 │      704 │ 1741660 │
├─────────────────────────┼───────┼─────────┼──────────┼──────────┼─────────┤
│ ArithPartition-z3-p16   │  5766 │    5705 │    11471 │      663 │ 1637352 │
╘═════════════════════════╧═══════╧═════════╧══════════╧══════════╧═════════╛
```

## Test Instances

Test instances are named in the format `theory-result_state-cost_time.smt2`, storing in `test-instances` dir.

`test-output-dir` is the temporary dir for instance-testing output, resulting in `lia-unsat-17.8.smt2`.

