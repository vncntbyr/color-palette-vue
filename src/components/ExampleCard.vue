<script setup lang="ts">
import type { Color } from 'chroma-js'
type CardProps = {
  textColor: Color | null
  backgroundColor: Color | null
  ctaBackgroundColor: Color | null
  ctaTextColor: Color | null
}

const { textColor, backgroundColor, ctaBackgroundColor, ctaTextColor } = defineProps<CardProps>()
const backgroundStyle = { 'background-color': backgroundColor?.hex() }
const textStyle = { color: textColor?.hex() }
const ctaStyle = { 'background-color': ctaBackgroundColor?.hex(), color: ctaTextColor?.hex() }
</script>

<template>
  <div class="rounded-md p-2 h-48 flex flex-col justify-between" :style="backgroundStyle">
    <div :style="textStyle">
      <h2>Card Title</h2>
      <span>This is a card</span>
    </div>
    <div class="flex justify-end">
      <button class="px-2 py-1 rounded-md" :style="ctaStyle">Buy now</button>
    </div>
  </div>
</template>

<style scoped>
/* Base styles */
.rounded-md {
  border-radius: 0.375rem; /* 6px */
}

.p-2 {
  padding: 0.5rem; /* 2px */
}

.h-48 {
  height: 12rem; /* 48px */
}

.flex {
  display: flex;
}

.flex-col {
  flex-direction: column;
}

.justify-between {
  justify-content: space-between;
}

.justify-end {
  justify-content: flex-end;
}
</style>
