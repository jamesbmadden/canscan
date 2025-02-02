<script setup>
defineProps({
  colour: {
    type: String,
    required: true,
  },
  gap: {
    type: String,
    required: true
  }
})
</script>

<template>
  <section class="section-frame">
    <slot></slot>
  </section>
</template>

<style scoped>
.section-frame {
  box-sizing: border-box;
  padding: 16px;
  position: relative;
  display: block;
  width: 100%;
  height: 100%;
  border-radius: 64px;
  background-color: v-bind(colour);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: v-bind(gap);
}
</style>