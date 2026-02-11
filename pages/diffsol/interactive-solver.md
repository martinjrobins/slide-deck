---
layout: default
---

# Demo: Compile to WebAssembly

<link rel="stylesheet" href="https://diffsol-js.fly.dev/interactive-solver.css" />

<div class="flex justify-center items-start">
  <div id="solver" class="w-7/8 h-full bg-white p-4 rounded-lg shadow-md"></div>
</div>


<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  // Load Plotly from CDN
  const plotlyScript = document.createElement('script')
  plotlyScript.src = 'https://cdn.plot.ly/plotly-2.26.0.min.js'
  
  plotlyScript.onload = () => {
    // Load DiffSol bundle
    const diffsolScript = document.createElement('script')
    diffsolScript.src = 'https://diffsol-js.fly.dev/diffsol.min.js'
    
    diffsolScript.onload = () => {
      // Access DiffSol from global namespace
      const { createInteractiveSolver, MatrixType, LinearSolverType, OdeSolverType } = window.DiffSol
      
      // Create interactive solver
      createInteractiveSolver({
        divId: 'solver',
        diffslCode: `
            in_i { r = 1, k = 1 }
            u { 0.05 }
            F { r * u * (1.0 - u / k) }
            out { u }
        `,
        sliders: [
          {
            label: 'Growth Rate (r)',
            min: 0.1,
            max: 20,
            initial: 10,
          },
          {
            label: 'Carrying Capacity (k)',
            min: 0.1,
            max: 5,
            initial: 10,
          },
        ],
        outputs: [
          { label: 'u(t)' },
        ],
        moduleConfig: {
          backendUrl: 'https://diffsol-js.fly.dev',
        },
        finalTime: 1.0,
        matrixType: MatrixType.FaerDense,
        linearSolverType: LinearSolverType.Lu,
        odeSolverType: OdeSolverType.Bdf,
        showCodeEditor: true,
        codeEditorTheme: 'github-light',
        codeEditorHeight: 'auto',
        showHelp: false,
        plotHeight: 200,
      })
    }
    
    document.head.appendChild(diffsolScript)
  }
  
  document.head.appendChild(plotlyScript)
})
</script>
