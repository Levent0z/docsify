# Introduction to NP-Completeness

`Undecidable problems`: A problem that can be shown to not be solvable by a computer. E.g. the `Halting problem`: "Is it possible for a program to check whether a program provided as input halts or not?".

$P$ = Polynomial Time

$NP$ = Non-deterministic Polynomial Time

- A problem is in $NP$ if it can be shown that any "yes" answer to a yes/no question is correct.
- Not all `decidable` problems are in $NP$. (e.g. Non-Hamiltonian Cycle)
- `NP-Complete` problems are those for which a given answer can be checked in polynomial time, but a solution can not be found in polynomial time.
- `NP-Complete` is a subset of `NP-Hard` (if $P \ne NP$)

The most basic NP-Complete problem is the `Satisfiability Problem`: "For a given boolean expression, is there a set of truth values to the variables that makes the expression true?"

`Traveling Salesman Problem`: (NP-complete)
"Given a complete weighted graph and K, is there a simple cycle that visits all vertices and has total cost <= K?"

To prove that a problem is NP-Complete:
1. It must be in $NP$
2. A known NP-Complete problem must be transformed into it