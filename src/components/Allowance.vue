<script setup>
import MoneyInput from './MoneyInput.vue'

const props = defineProps({
  allowance: Number
})

const emit = defineEmits('update:allowance')
</script>

<template>
  <div class="results-container">
    <h2>お小遣い</h2>
    <div class="card">
      <MoneyInput
        label="お小遣い（1人分）"
        :modelValue="allowance"
        @update:modelValue="v => emit('update:allowance', v)"
      />
    </div>
  </div>
</template>
