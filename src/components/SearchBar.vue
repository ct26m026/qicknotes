<script setup>
defineProps(['modelValue'])

defineEmits(['update:modelValue'])
</script>

<template>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    placeholder="Suchen ..."
  >
</template>

<style scoped>
input {
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 6px;
}
</style>