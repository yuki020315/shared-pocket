<script setup>

import MoneyResult from './MoneyResult.vue'
import MoneyResultShare from './MoneyResultShare.vue'


const props = defineProps({
  resultA: Number,
  resultB: Number,
  sharedTotal: Number
})

const emit = defineEmits(['update:resultA','update:resultB','update:sharedTotal'])

</script>


<template>
  <div class="results-container">
    <h2>収支</h2>
    <div class="results">
      <MoneyResult
        name="Aさん"
        :value="resultA" 
      />
      <MoneyResult
        name="Bさん"
        :value="resultB"
      />
      <MoneyResultShare
        name="共有口座"
        :value="sharedTotal"
      />
    </div>
  </div>
</template>
