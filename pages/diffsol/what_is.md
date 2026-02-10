---
level: 2
---

<div class="w-full flex justify-center">
  <img class="block" src="/diffsol_rectangle.svg" alt="diffsol logo" />
</div>

# What is it?

Diffsol is a library for solving ordinary differential equations (ODEs) or semi-explicit differential algebraic equations (DAEs) in Rust. It can solve equations in the following form:

$$
\begin{align*}
M \frac{dy}{dt} &= f(t, y, p) \\
y(0) &= y_0(p) \\
\end{align*}
$$

where 

- $M$ is a (possibly singular and optional) mass matrix, 
- $y$ is the state vector, 
- $t$ is the time and 
- $p$ is a vector of parameters.

