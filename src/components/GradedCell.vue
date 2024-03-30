<script setup lang="ts">
import { getChromaColor } from '../utils'
import type { ColorGrade } from '../types'

type ColorGradeProps = {
  grade: ColorGrade
  lAxis: number
  chroma: number
  hue: number
}

const { grade, lAxis, chroma, hue } = defineProps<ColorGradeProps>()

const color = getChromaColor({ lAxis, chroma, hue })
const hexColor = color?.hex()
// TODO: this does not work dynamically as it seems
const textColor = `${lAxis > 0.5 ? { color: '000' } : { color: 'fff' }}`
const backgroundColor = { backgroundColor: hexColor }
</script>

<template>
  <div class="flex flex-1 flex-col w-10-12 px-1" :style="backgroundColor">
    <div class="flex flex-1 justify-between">
      <div class="flex items-end" :style="textColor">
        <span>.{{ grade }}</span>
      </div>
      <div class="flex flex-col justify-end items-end gap-1">
        <span>{{ hexColor }}</span>
        <span> oklch({{ lAxis }}, {{ chroma }}, {{ hue }}) </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.flex {
  display: flex;
}

.flex-1 {
  flex: 1;
}

.flex-col {
  flex-direction: column;
}

.w-10-12 {
  width: 83.333333%;
}

.px-1 {
  padding-left: 0.25rem;
  padding-right: 0.25rem;
}

.justify-between {
  justify-content: space-between;
}

.justify-end {
  justify-content: flex-end;
}

.items-end {
  align-items: flex-end;
}
</style>
