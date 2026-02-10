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
layout: center
class: text-center
---

# Qustions?

[Diffsol book](https://martinjrobins.github.io/diffsol/) · [GitHub](https://github.com/martinjrobins/diffsol)

Martin Robinson

Oxford Research Software Engineering Group

Doctoral Training Centre

University of Oxford

martin.robinson@dtc.ox.ac.uk
