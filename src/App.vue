<script setup>
import { ref, computed } from 'vue'
import AppHeader from './components/Header.vue'
import Income from './components/Income.vue'
import Result from './components/Result.vue'
import Allowance from './components/Allowance.vue'

// --- 状態を親で管理 ---
const allowance = ref(0)
const incomesA = ref([0])
const incomesB = ref([0])
const incomesShare = ref([0])

// --- 計算 ---
const totalA = computed(() => incomesA.value.reduce((sum, v) => sum + v, 0))
const totalB = computed(() => incomesB.value.reduce((sum, v) => sum + v, 0))
const totalSheare = computed(() => incomesShare.value.reduce((sum, v) => sum + v, 0))

const resultA = computed(() => (totalA.value - allowance.value) * 10000)
const resultB = computed(() => (totalB.value - allowance.value) * 10000)
const sharedTotal = computed(() => (totalA.value + totalB.value - allowance.value * 2 - totalSheare.value) * 10000)

</script>

<template>
  <div class="app">
    <AppHeader />

    <main class="content">
      <Income
        v-model:incomesA="incomesA"
        v-model:incomesB="incomesB"
        v-model:incomesShare="incomesShare"
      />

      <Allowance
        v-model:allowance="allowance"
      />

      <Result 
        v-model:resultA="resultA"
        v-model:resultB="resultB"
        v-model:sharedTotal="sharedTotal"
      />
    </main>
  </div>
</template>

<style scoped>
.app {
  background: #f5f7fb;
  min-height: 100vh;
}

.content {
  max-width: 1000px;
  margin: auto;
  padding: 16px;
}
</style>
