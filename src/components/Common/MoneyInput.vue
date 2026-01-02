<script setup>
defineProps({
  modelValue: Number,
  label: String
})

defineEmits(['update:modelValue'])
</script>

<template>
  <div class="money-input">
    <span class="label">{{ label }}</span>

    <div class="input-wrap">
      <input
        type="number"
        min="0"
        step="1"
        :value="modelValue"
        @input="$emit('update:modelValue', Number($event.target.value))"
      />
      <span class="unit">万円</span>
    </div>
  </div>
</template>

<style scoped>
.money-input {
  display: flex;
  align-items: center;
  gap: 8px;
}

.label {
  min-width: 60px;
}

.input-wrap {
  display: flex;
  align-items: center;
  gap: 4px;
}

input {
  width: 90px;
  padding: 6px;
  border-radius: 6px;
  border: 1px solid #ccc;
}
</style>
