<script setup lang="ts">
type InputSliderProps = {
  hue: number
  onRangeChanged: (e: Event) => void
}
const { hue } = defineProps<InputSliderProps>()
</script>

<template>
  <div class="flex-col">
    <input type="range" min="0" max="360" :value="hue" @input="onRangeChanged" />
    <span>hue: {{ hue }}</span>
  </div>
</template>

<style scoped>
.flex-col {
  display: flex;
  flex-direction: column;
}
</style>
