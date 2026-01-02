<script setup>
import { computed } from 'vue'
import MoneyInput from '../Common/MoneyInput.vue'

const props = defineProps({
  incomes: Array,
  title: String
})

const emit = defineEmits(['update'])

const addIncome = () => {
  emit('update', [...props.incomes, 0])
}

const removeIncome = (index) => {
  const copy = [...props.incomes]
  copy.splice(index, 1)
  emit('update', copy)
}

const updateIncome = (index, value) => {
  const copy = [...props.incomes]
  copy[index] = value
  emit('update', copy)
}

const total = computed(() =>
  props.incomes.reduce((sum, v) => sum + v, 0)
)
</script>

<template>
  <div class="card">
    <h3>{{ title }}</h3>

    <div
      v-for="(income, i) in incomes"
      :key="i"
      class="income-row"
    >
      <MoneyInput
        :label="`収入${i + 1}`"
        :modelValue="income"
        @update:modelValue="v => updateIncome(i, v)"
      />

      <button
        class="remove-btn"
        v-if="incomes.length > 1"
        @click="removeIncome(i)"
      >
        −
      </button>
    </div>

    <button class="add-btn" @click="addIncome">＋</button>

    <p class="total">合計：{{ total }} 万円</p>
  </div>
</template>

<style scoped>
.income-row {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 8px;
}

.add-btn {
  background: #e0e7ff;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
}

.remove-btn {
  background: #fee2e2;
  border: none;
  border-radius: 6px;
  padding: 4px 10px;
  cursor: pointer;
}

.total {
  margin-top: 8px;
  font-weight: bold;
}
</style>
