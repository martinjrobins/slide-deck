# Implementation in Python

```python
class MyModel(pints.Model):
    def n_parameters(self):
        ...
    
    def simulate(self, parameters, times):
        ...
        return simulated_values

problem = SingleOutputProblem(model, times, measured_values)
error_measure = SumOfSquaresError(problem)
log_likelihood = GaussianLogLikelihood(problem)

optimisation = OptimisationController(error_measure, initial_point)
mcmc = MCMCController(log_likelihood, n_chains, initial_points)

best_parameters = optimisation.run()
chains = mcmc.run()
```
