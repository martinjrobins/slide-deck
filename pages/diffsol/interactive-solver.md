---
layout: default
---

# Demo: Compile to WebAssembly

<link rel="stylesheet" href="https://diffsol-js.fly.dev/interactive-solver.css" />

<div class="flex justify-center items-start">
  <div id="solver" class="w-3/4 h-full bg-white p-4 rounded-lg shadow-md"></div>
</div>

<style>
.diffsol-interactive-solver-container {
  display: flex;
  flex-direction: column;
  height: 100%;
  gap: 8px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.diffsol-interactive-solver-plot {
  flex: 1;
  min-height: 250px;
  border-radius: 6px;
  border: 1px solid #e5e7eb;
  overflow: hidden;
}

.diffsol-interactive-solver-error {
  flex: 1;
  min-height: 250px;
  padding: 16px;
  background-color: #fee2e2;
  border: 1px solid #fca5a5;
  border-radius: 6px;
  color: #991b1b;
  overflow: auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.diffsol-interactive-solver-code-panel {
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: 8px;
  flex: 0 0 auto;
  height: 90px;
}

.diffsol-interactive-solver-code-editor-container {
  display: flex;
  flex-direction: column;
  border-radius: 6px;
  border: 1px solid #e5e7eb;
  overflow: hidden;
  background: #f9fafb;
}

.diffsol-interactive-solver-code-editor {
  flex: 1;
  overflow: auto;
  font-size: 9px;
  font-family: 'Courier New', monospace;
  line-height: 1.3;
  padding: 6px;
}

.diffsol-interactive-solver-sliders {
  display: flex;
  flex-direction: column;
  gap: 6px;
  padding: 8px;
  border-radius: 6px;
  border: 1px solid #e5e7eb;
  background: #f9fafb;
  overflow: auto;
}

.diffsol-interactive-solver-slider-group {
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.diffsol-interactive-solver-label {
  font-weight: 500;
  font-size: 11px;
  color: #374151;
}

.diffsol-interactive-solver-slider-row {
  display: flex;
  align-items: center;
  gap: 6px;
}

.diffsol-interactive-solver-input {
  flex: 1;
  height: 5px;
  cursor: pointer;
  accent-color: #6366f1;
}

.diffsol-interactive-solver-value {
  min-width: 50px;
  text-align: right;
  font-size: 11px;
  font-weight: 500;
  color: #374151;
  font-variant-numeric: tabular-nums;
}

.diffsol-interactive-solver-compile-button {
  padding: 8px 16px;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  color: white;
  border: none;
  border-radius: 6px;
  font-weight: 600;
  font-size: 12px;
  cursor: pointer;
  transition: all 0.2s ease;
  width: auto;
}

.diffsol-interactive-solver-compile-button:hover {
  box-shadow: 0 4px 12px rgba(99, 102, 241, 0.4);
  transform: translateY(-1px);
}

.diffsol-interactive-solver-help-button {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  flex-shrink: 0;
}

.diffsol-interactive-solver-help-button:hover {
  box-shadow: 0 4px 12px rgba(99, 102, 241, 0.4);
  transform: scale(1.1);
}
</style>

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
