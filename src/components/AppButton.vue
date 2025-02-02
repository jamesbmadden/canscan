<script setup>
defineProps({
  label: {
    type: String,
    required: true,
  }
})
</script>

<template>
  <button class="app-button">
    <span class="button-label body">{{ label }}</span>
  </button>
</template>

<style scoped>
.app-button {
  display: inline-flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 0px;
  gap: 8px;
  width: 256px;
  height: 64px;
  background: #DD6868; /* use the current colour theme */
  color: white;
  border-radius: 32px;
  border: none;
  cursor: pointer;
  transition: transform 0.1s;
}
.app-button:hover {
  transform: translateY(-2px);
}
</style>