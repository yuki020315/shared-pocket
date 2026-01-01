<script setup>
import { ref, computed } from 'vue'
import IncomeList from './components/IncomeList.vue'
import MoneyInput from './components/MoneyInput.vue'
import MoneyResult from './components/MoneyResult.vue'
import MoneyResultShere from './components/MoneyResultShare.vue'

const allowance = ref(0)

const incomesA = ref([0])
const incomesB = ref([0])
const incomesSheare = ref([0])


const totalA = computed(() =>
  incomesA.value.reduce((sum, v) => sum + v, 0)
)

const totalB = computed(() =>
  incomesB.value.reduce((sum, v) => sum + v, 0)
)

const totalSheare = computed(() =>
  incomesSheare.value.reduce((sum, v) => sum + v, 0)
)

const resultA = computed(() =>
  (totalA.value - allowance.value) * 10000
)

const resultB = computed(() =>
  (totalB.value - allowance.value) * 10000
)

const resultSheare = computed(() =>
  (totalSheare.value) * 10000
)

const sharedTotal = computed(() =>
  (totalA.value + totalB.value
   - allowance.value * 2
   - totalSheare.value) * 10000
)
</script>

<template>
  <div class="app">
    <!-- ヘッダー -->
    <header class="header">
      <h1>共有口座調整ツール</h1>
    </header>

    <main class="content">
      <div class="results-container">
        <h2>各自の共有口座調整</h2>   <!-- タイトル -->
        <div class="results">
          <IncomeList
            title="Aさん"
            :incomes="incomesA"
            @update="v => incomesA = v"
          />
          <IncomeList
            title="Bさん"
            :incomes="incomesB"
            @update="v => incomesB = v"
          />
          <IncomeList
            title="支出"
            :incomes="incomesSheare"
            @update="v => incomesSheare = v"
          />
        </div>
      </div>

      <div class="results-container">
        <h2>お小遣い</h2>   <!-- タイトル -->
        <div class="card">
          <MoneyInput label="お小遣い（1人分）" v-model="allowance" />
        </div>
      </div>

      <div class="results-container">
        <h2>収支</h2>   <!-- タイトル -->
        <div class="results">
          <MoneyResult name="Aさん" :value="resultA" />
          <MoneyResult name="Bさん" :value="resultB" />
          <MoneyResultShere name="共有口座" :value="sharedTotal" />
        </div>
      </div>
      
    </main>
  </div>
</template>

<style scoped>
.app {
  background: #f5f7fb;
  min-height: 100vh;
}

.header {
  width: 100%;
  background: linear-gradient(90deg, #4f46e5, #6366f1);
  color: white;
  padding: 16px 24px;
}

.content {
  max-width: 1000px;
  margin: auto;
  padding: 16px;
}

</style>
