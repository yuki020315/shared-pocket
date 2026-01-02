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
      共有口座は<strong>{{ abs(value) }} 円</strong> 増加
    </p>
    <p v-else>
      共有口座は <strong>{{ abs(value) }} 円</strong> 減少
    </p>
  </div>
</template>
