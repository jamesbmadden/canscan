<script setup>
import CheckIcon from 'vue-material-design-icons/Check.vue'
import CrossIcon from 'vue-material-design-icons/Close.vue'
import EarthIcon from 'vue-material-design-icons/Earth.vue'
import SectionFrame from './SectionFrame.vue'

defineProps({
  /*
  * state options:
  * 0 = loading,
  * 1 = canada,
  * 2 = usa,
  * 3 = international
  */
  state: {
    type: Number,
    required: true,
  }
})
</script>

<template>
  <SectionFrame v-if="state == 1" colour="#DD6868" gap="16px" class="result result--canada">
    <CheckIcon fillColor="#FFFFFF" :size="196"></CheckIcon>
    <h1 class="subtitle">Made In Canada!</h1>
    <p class="body">Buy Canadian with this product!</p>
  </SectionFrame>
  <SectionFrame v-else-if="state == 2" colour="#687DDD" gap="16px" class="result result--usa">
    <CrossIcon fillColor="#FFFFFF" :size="196"></CrossIcon>
    <h1 class="subtitle">Made In The US</h1>
    <p class="body">Avoid this product if you can.</p>
  </SectionFrame>
  <SectionFrame v-else-if="state == 3" colour="#9368DD" gap="16px" class="result result--international">
    <EarthIcon fillColor="#FFFFFF" :size="196"></EarthIcon>
    <h1 class="subtitle">International Product</h1>
  </SectionFrame>
</template>

<style scoped>
.result {
  color: white;
}
</style>