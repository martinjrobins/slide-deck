---
level: 4
---

# Example: The logistic growth model

$$
\begin{align*}
\frac{dy}{dt} &= r \cdot y \cdot \left(1 - \frac{y}{k}\right) \\
y(0) &= 0.1 \\
\end{align*}
$$

Using Rust closures:

```rust
type M = diffsol::NalgebraMat<f64>;
type LS = diffsol::NalgebraLU;

let problem = diffsol::OdeBuilder::<M>::new()
    .p(vec![1.0, 10.0])
    .rhs_implicit(
        |x, p, _t, y| y[0] = p[0] * x[0] * (1.0 - x[0] / p[1]),
        |x, p, _t, v, y| y[0] = p[0] * v[0] * (1.0 - 2.0 * x[0] / p[1]),
    )
    .init(|_p, _t, y| y.fill(0.1), 1)
    .build()
    .unwrap()
let mut solver = problem.bdf::<LS>().unwrap();
let (ys, ts) = solver.solve(40.0).unwrap();
```

