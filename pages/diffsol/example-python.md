---
---

# Example: The logistic growth model

$$
\begin{align*}
\frac{dy}{dt} &= r \cdot y \cdot \left(1 - \frac{y}{k}\right) \\
y(0) &= 0.1 \\
\end{align*}
$$

Using [pydiffsol](https://github.com/alexallmont/pydiffsol), the Python bindings for Diffsol (`pip install pydiffsol`):

```python
import pydiffsol as ds

ode = ds.Ode("""
    in = [r, k]
    r { 1.0 } k { 1.0 }
    u { 0.1 }
    F { r * u * (1.0 - u / k) }
    """,
    scalar_type=ds.f64, matrix_type=ds.nalgebra_dense,
    linear_solver=ds.lu, method=ds.bdf,
)
ode.rtol = 1e-6
params = np.array([1.0, 10.0])
ys, ts = ode.solve(params, 40.0)
```