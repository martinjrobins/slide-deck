---
level: 3
---
# Features

**Solver Methods**:

1. A variable order Backwards Difference Formulae (BDF) solver
1. A Singly Diagonally Implicit Runge-Kutta (SDIRK or ESDIRK) solver (TR-BDF2 and ESDIRK34 tableaus)
1. A variable order Explict Runge-Kutta (ERK) solver (TSIT45 tableau)

**Solver Options**:

1. Matrices, vectors and solvers from the `nalgebra` or `faer` crates
1. Adaptive step-size error control with dense output
1. High-level "solve" API or manual time-stepping, event handling, etc.
1. Numerical quadrature of an optional output function $g(t, y, p)$
1. Forwards and adjoint sensitivity analysis

