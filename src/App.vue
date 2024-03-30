<script setup lang="ts">
import { ref } from 'vue'
import InputSlider from './components/InputSlider.vue'
import ExampleCard from './components/ExampleCard.vue'
import GradedCell from './components/GradedCell.vue'
import type { ColorGrade, CustomColor } from './types'
import { getColor, getColorRanges, getKeys } from './utils'

const hue = ref<number>(0)

const colorGrades: ColorGrade[] = ['100', '200', '300', '400', '500', '600', '700', '800', '900']
// TODO: this does not seem to get recalculated when hue changes
const colors: Record<ColorGrade, CustomColor> = getColor(colorGrades, hue.value)
const colorRanges = getColorRanges(colors)
const colorRangeKeys = getKeys(colorRanges)
const colorKeys = getKeys(colors)

function onRangeChanged(e: Event) {
  hue.value = parseInt((e.target as HTMLInputElement).value)
}
</script>

<template>
  <main>
    <div id="leftSide">
      <InputSlider :hue :on-range-changed="onRangeChanged" />
      <div id="examples">
        <ExampleCard
          v-for="variant of colorRangeKeys"
          :key="variant"
          :text-color="colorRanges[variant].textColor"
          :background-color="colorRanges[variant].backgroundColor"
          :cta-background-color="colorRanges[variant].ctaBackgroundColor"
          :cta-text-color="colorRanges[variant].ctaTextColor"
        />
      </div>
    </div>
    <div id="rightSide">
      <div id="colorGrades">
        <GradedCell
          v-for="grade of colorKeys"
          :key="grade"
          :grade="grade"
          :l-axis="colors[grade].lAxis"
          :chroma="colors[grade].chroma"
          :hue="colors[grade].hue"
        />
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  background-color: white;
  color: black;
  display: flex;
  flex: 1;
  justify-content: space-between;
  height: 100vh;
  padding: 2rem;
}
#leftSide {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 50%;
  gap: 1rem;
}
#examples {
  display: flex;
  gap: 1.5rem;
  flex-direction: column;
}
#rightSide {
  display: flex;
  width: 50%;
}
#colorGrades {
  display: flex;
  flex-direction: column;
  padding: 0 1rem;
  align-items: center;
  flex: 1;
}
</style>
