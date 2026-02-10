---
level: 3
---

# Example: The logistic growth model

$$
\begin{align*}
\frac{dy}{dt} &= r \cdot y \cdot \left(1 - \frac{y}{k}\right) \\
y(0) &= 0.1 \\
\end{align*}
$$

Using DiffSL DSL:

```rust
type M = diffsol::NalgebraMat<f64>;
type LS = diffsol::NalgebraLU;
type CG = diffsol::LlvmModule;

let problem = diffsol::OdeBuilder::<M>::new()
    .p(vec![1.0, 10.0])
    .build_from_diffsl::<CG>(
        "
        in = [r, k]
        r { 1.0 } k { 1.0 }
        u { 0.1 }
        F { r * u * (1.0 - u / k) }
        ",
    ).unwrap();
let mut solver = problem.bdf::<LS>().unwrap();
let (ys, ts) = solver.solve(40.0).unwrap();
```

