<script setup>
import { ref, computed } from 'vue'
import Problems from './components/Promblems.vue'
import InputArea from './components/InputArea.vue'
import NavBar from './components/NavBar.vue'
import Diagram from './components/DFAVisualization.vue'
import PDAVisualization from './components/PDAVisualization.vue'
import CFGVisualization from './components/CFGVisualization.vue'
import Footer from './components/Footer.vue'

const activeAutomata = ref('dfa')
const simulationInputs = ref([])

const automata = ref('automata-theory project')

const problems = ref([
  {
    id: 1,
    label: '(bab+bbb) b* a* (a*+b*) (ab)* (aba) (bab+aba)* bb (a+b)* (bab+aba) (a+b)*',
    regexStr: '(bab+bbb) b* a* (a*+b*) (ab)* (aba) (bab+aba)* bb (a+b)* (bab+aba) (a+b)*'
  },
  {
    id: 2,
    label: '(1+0)* 0* 1* (111+00+101) (1+0)* (101+01+000) (1+0)* (101+000)*',
    regexStr: '(1+0)* 0* 1* (111+00+101) (1+0)* (101+01+000) (1+0)* (101+000)*'
  }
])

const selectedProblemIndex = ref(-1)
const currentRegex = computed(() => {
    if (selectedProblemIndex.value === -1) return ''
    return problems.value[selectedProblemIndex.value]?.regexStr || ''
})

const updateSimulationInputs = (newInputs) => {
  simulationInputs.value = newInputs
}

const currentTestString = ref('')
const simulationKey = ref(0)
const runSimulation = (str) => {
  currentTestString.value = str
  simulationKey.value++
}
</script>

<template>
  <NavBar />
  
  <div class="main-container">
    <div class="main-title">
      <h1>{{ automata }}</h1>
      <p>Interactive Regular Expressions Simulator</p>
    </div>

    <!-- Problem Selection Section -->
    <div class="selection-section">
      <div class="card">
        <div class="card-header">Select a Regular Expression</div>
        <div class="card-body">
          <Problems 
            :problems="problems" 
            v-model="selectedProblemIndex" 
          />
        </div>
      </div>
    </div>

    <!-- Testing & Visualization Section (shown only after selection) -->
    <template v-if="selectedProblemIndex !== -1">
      <div class="content-section">
        <!-- Testing Area -->
        <div class="card">
          <div class="card-header">Test Strings</div>
          <div class="card-body">
            <InputArea 
              :regexStr="currentRegex" 
              @inputs-updated="updateSimulationInputs" 
              @simulate-string="runSimulation" 
            />
          </div>
        </div>

        <!-- Visualization Controls -->
        <div class="card card-controls">
          <button 
            :class="{ active: activeAutomata === 'dfa' }"
            @click="activeAutomata = 'dfa'"
          >
            DFA
          </button>
          <button 
            :class="{ active: activeAutomata === 'cfg' }"
            @click="activeAutomata = 'cfg'"
          >
            CFG
          </button>
          <button 
            :class="{ active: activeAutomata === 'pda' }"
            @click="activeAutomata = 'pda'"
          >
            PDA
          </button>
        </div>

        <!-- Visualization -->
        <div class="card card-lg">
          <div v-if="activeAutomata === 'dfa'">
            <Diagram 
              :problemId="problems[selectedProblemIndex].id" 
              :testString="currentTestString" 
              :simKey="simulationKey" 
            />
          </div>
          <div v-else-if="activeAutomata === 'cfg'">
            <CFGVisualization 
              :problemId="problems[selectedProblemIndex].id" 
              :testString="currentTestString" 
            />
          </div>
          <div v-else-if="activeAutomata === 'pda'">
            <PDAVisualization 
              :problemId="problems[selectedProblemIndex].id" 
            />
          </div>
        </div>
      </div>
    </template>
  </div>

  <Footer />
</template>

<style scoped>
.main-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 16px;
}

.main-title {
  text-align: center;
  padding: 40px 16px 24px;
  background: linear-gradient(180deg, rgba(88, 166, 255, 0.1) 0%, transparent 100%);
  border-bottom: 1px solid #30363d;
  margin-bottom: 32px;
}

.main-title h1 {
  margin: 0 0 12px 0;
  background: linear-gradient(90deg, #58a6ff, #79c0ff, #58a6ff);
  background-size: 200% auto;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: shimmer 3s ease-in-out infinite;
}

@keyframes shimmer {
  0%, 100% { background-position: 0% center; }
  50% { background-position: 100% center; }
}

.main-title p {
  text-align: center;
  font-size: 1rem;
  font-weight: 400;
  color: #8b949e;
  margin: 0;
  letter-spacing: 0.5px;
}

/* Minimalist sections */
.selection-section {
  margin-bottom: 40px;
}

.content-section {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Control Buttons */
.card-controls {
  padding: 16px;
  justify-content: center;
  gap: 12px;
  display: flex;
  flex-wrap: wrap;
}

.card-controls button {
  padding: 10px 20px;
  border-radius: 6px;
  border: 1px solid #30363d;
  background: #21262d;
  color: #79c0ff;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  min-width: 80px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.card-controls button:hover {
  border-color: #58a6ff;
  background: #30363d;
  color: #58a6ff;
  box-shadow: 0 0 10px rgba(88, 166, 255, 0.2);
}

.card-controls button.active {
  background: #238636;
  color: #ffffff;
  border-color: #3fb950;
  box-shadow: 0 0 15px rgba(63, 185, 80, 0.3);
}

.card-controls button.active:hover {
  background: #2ea043;
  box-shadow: 0 0 20px rgba(63, 185, 80, 0.4);
}

@media (max-width: 1000px) {
  .main-title {
    padding: 32px 16px 20px;
    margin-bottom: 24px;
  }

  .content-section {
    gap: 16px;
  }
}

@media (max-width: 480px) {
  .card-controls button {
    padding: 8px 14px;
    font-size: 12px;
    flex: 1;
  }
}
</style>