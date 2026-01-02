<script setup>
import IncomeList from './IncomeList.vue'

const props = defineProps({
  incomesA: Array,
  incomesB: Array,
  incomesShare: Array
})

const emit = defineEmits(['update:incomesA','update:incomesB','update:incomesShare'])
</script>

<template>
  <div class="results-container">
    <h2>各自の共有口座調整</h2>
    <div class="results">
      <IncomeList
        title="Aさん"
        :incomes="incomesA"
        @update="v => emit('update:incomesA', v)"
      />
      <IncomeList
        title="Bさん"
        :incomes="incomesB"
        @update="v => emit('update:incomesB', v)"
      />
      <IncomeList
        title="支出"
        :incomes="incomesShare"
        @update="v => emit('update:incomesShare', v)"
      />
    </div>
  </div>
</template>

<style scoped>
.results {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}
</style>
