---
# You can also start simply with 'default'
theme: dracula
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: OxRSE, modelling & model fitting with time series data
info: |
  Martin Robinson  
  Oxford Research Software Engineering Group  
  Doctoral Training Centre  
  University of Oxford
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
---

# OxRSE: ODE modelling/fitting with diffsol and PINTS

 https://www.rse.ox.ac.uk/

Martin Robinson 

Oxford Research Software Engineering Group

Doctoral Training Centre

University of Oxford


<div class="abs-br m-6 text-xl">
  <a href="https://github.com/martinjrobins/diffsol" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
level: 1
---

# Contents

1. OxRSE, who we are and what we do
1. Diffsol, a Rust library for solving ODEs/DAEs
1. PINTS, a Python library for fitting models to time series data


---
src: ./pages/front_page.md
---

---
src: ./pages/mission_people_law_ai_April2025.md
---

---
src: ./pages/portfolio.md
---

---
src: ./pages/portfolio_data_platforms_intro.md
---

---
src: ./pages/portfolio_apps_intro.md
---

---
src: ./pages/portfolio_modelling_intro.md
---


---
src: ./pages/training.md
---

---
layout: default
---

<div class="grid grid-cols-2 items-center justify-center h-full">
    <div class="grid-col-span-1">
        <h3><a href="https://www.rse.ox.ac.uk/contact.html">www.rse.ox.ac.uk/contact.html</a></h3>
        <img class="w-full shadow-md mt-5" src="/get_in_touch.png" alt="Funding model"/>
    </div>
    <div class="grid-col-span-1 mt-10 ml-10 h-full">
        <h1 class="font-semibold">Funding Model:</h1>
        <h2 class="font-medium mt-10">Internal/Academic:</h2>
        <h3 class="italic ml-5">Costed into grants (grade 8.3) or SRF with day rate</h3>
        <h2 class="font-medium mt-10">Commercial:</h2>
        <h3 class="italic ml-5">consultancy contract via Oxford University Innovation</h3>
    </div>
</div>

---

# Diffsol and PINTS

- **Diffsol: a Rust library for solving ODEs/DAEs, with Python bindings (pydiffsol)**
  - Robinson, M., & Allmont, A. (2026). diffsol: Rust crate for solving differential equations. Journal of Open Source Software, 11(117), 9384. https://doi.org/10.21105/joss.09384
- **PINTS: a Python library for fitting models to time series data**
  - Clerx, M., Robinson, M., Lambert, B., Lei, C., Ghosh, S., Mirams, G., & Gavaghan, D. (2019). Probabilistic inference on noisy time series (PINTS). Journal of Open Research Software, 7(1). https://doi.org/10.5334/jors.252 

---
src: ./pages/diffsol/what_is.md
---

---
src: ./pages/diffsol/features.md
---

---
src: ./pages/diffsol/provide.md
---

---
src: ./pages/diffsol/example-diffsl.md
---

---
src: ./pages/diffsol/example-closure.md
---

---
src: ./pages/diffsol/example-python.md
---


---
src: ./pages/diffsol/benchmarks-python.md
---

---
src: ./pages/diffsol/benchmarks-python-lotka-volterra.md
---


---
src: ./pages/diffsol/benchmarks-python-robertson.md
---

---
src: ./pages/diffsol/interactive-solver.md
---

---
layout: default
class: text-left
---

# PINTS Background

In many situations, we have a model with parameter values that we need to infer from noisy time-series data.

**PINTS** stands for **P**robabilistic **I**nference on **N**oisy **T**ime-**S**eries.

It is a Python-based tool to tackle inference problems within a probabilistic framework.

<a href="https://github.com/pints-team/pints" target="_blank">Free PINTS! https://github.com/pints-team/pints</a>

```bash
pip install pints
```

---
layout: two-cols
---

# Problem Statement

Given:
- Noisy experimental time series data
- A forward model with $d$ parameters that can predict values for a given set of times

We want to:
- Find the best set of parameters (optimisation)
- Explore their likelihood (sampling)

::right::
![](/pints/problem-statement-1.png)


---

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

---

# What's in PINTS?

- Samplers
- Optimisers
- Likelihoods and error functions
- Toy problems and distributions
- Diagnostic plots
- Documentation & Examples

---
layout: two-cols
---

# Optimisers

**Gradient-free methods:**
- CMAES (Hansen et al., 2006)
- XNES (Glasmachers et al., 2010)
- SNES (Schaul et al., 2011)
- PSO (Kennedy & Eberhart, 1995)
- Nelder-Mead simplex method (Nelder & Mead, 1965)
- SHGO (planned)

**Gradient-based methods:**
- Gradient descent
- BFGS (planned)

::right::

![](/pints/samplers-1.png)



---

# Likelihoods and Error Functions

<img src="/pints/likelihoods-and-error-functions-0.png" class="w-full max-h-[80%] object-contain" />

---
layout: two-cols
---

# Diagnostic Plots

<img src="/pints/diagnostic-plots-0.png" class="w-full max-h-[40%] object-contain mb-3" />

<img src="/pints/diagnostic-plots-2.png" class="w-full max-h-[40%] object-contain" />

::right::
<img src="/pints/diagnostic-plots-1.png" class="w-full max-h-[80%] object-contain" />

---
layout: two-cols
---

# Documentation & Examples

<img src="/pints/documentation-examples-0.png" class="w-full max-h-[35%] object-contain mb-3" />

<img src="/pints/slide-22-image-0.png" class="w-full max-h-[35%] object-contain" />

::right::

<img src="/pints/slide-21-image-0.png" class="w-full max-h-[35%] object-contain mb-3" />

<img src="/pints/slide-24-image-0.png" class="w-full max-h-[35%] object-contain" />

---
layout: two-cols
---

# Qustions?

Thanks for listening!

![Oxford RSE logos](/2024_oxrse_next_to_oxford.svg){style="height: 10rem;"}

## Links:

- OxRSE: https://www.rse.ox.ac.uk
- DiffSL: <https:://github.com/martinjrobins/diffsl>
- diffsol: https://github.com/martinjrobins/diffsol
- pydiffsol: https://github.com/alexallmont/pydiffsol
- PINTS: https://github.com/pints-team/pints

::right::

## Contact:

Martin Robinson <mailto:martin.robinson@dtc.ox.ac.uk>
Oxford Research Software Engineering Group

## These slides:

<https://martinjrobins.github.io/slide-deck>

<div class="flex justify-center items-center">
  <a href="https://martinjrobins.github.io/slide-deck" target="_blank">
    <img src="https://api.qrserver.com/v1/create-qr-code/?size=400x400&data=https://martinjrobins.github.io/slide-deck" alt="QR code to slide deck" class="w-70 h-70" />
  </a>
</div>
