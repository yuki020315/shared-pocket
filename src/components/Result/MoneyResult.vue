<script setup>
defineProps({
  name: String,
  value: Number
})

const abs = v => Math.abs(v).toLocaleString()
</script>

<template>
  <div class="card">
    <h3>{{ name }}</h3>

    <p v-if="value >= 0">
      共有口座に <strong>{{ abs(value) }} 円</strong> 支払う
    </p>
    <p v-else>
      共有口座から <strong>{{ abs(value) }} 円</strong> 受け取る
    </p>
  </div>
</template>
