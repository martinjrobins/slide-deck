---
---

# Python ODE Solver Benchmarks

We benchmark the Python bindings for Diffsol, comparing:

- [Diffsol's](https://github.com/martinjrobins/diffsol) BDF, ESDIRK34, TR-BDF2, TSIT45 methods
- [CasADi's](https://web.casadi.org/) CVODE solver
- [Diffrax's](https://github.com/patrick-kidger/diffrax) Kvaerno5 & Tsit5 solvers
- Julia’s [DifferentialEquations.jl](https://diffeq.sciml.ai/stable/) FBDF, KenCarp3, TRBDF2 & Tsit5 methods

<div class="grid grid-cols-2 gap-4">
<div>

**Lotka-Volterra**

Non-stiff predator-prey model (*vary tolerance*):

$$
\begin{align*}
   \frac{dx}{dt} &= a x - b xy \\
   \frac{dy}{dt} &= c xy - d y
\end{align*}
$$

where $x$ is the number of prey, $y$ is the number of predators.

</div>
<div>

**Robertson (1966)**

Stiff autocatalytic reaction (*vary size* by creating multiple independent groups):

$$
   \begin{align}
   \frac{dx}{dt} &= -0.04x + 10^4 y z \\
   \frac{dy}{dt} &= 0.04x - 3 \cdot 10^7 y^2 - 10^4 y z \\
   \frac{dz}{dt} &= 3 \cdot 10^7 y^2 \\
   \end{align}
$$

Known to be stiff due to widely varying timescales.

</div>
</div>

We can extend this problem to a larger system by creating multiple independent groups of the Robertson equations,