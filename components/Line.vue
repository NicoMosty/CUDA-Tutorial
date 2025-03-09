<!--

Simple line

<Line x1="10" y1="20" x2="100" y2="200" color="green" width="3" />

<Line v-bind="{ x1:10, y1:10, x2:200, y2:200 }"/>

-->


<template>
  <svg class="absolute left-0 top-0 z-100" :width="Math.max(+x1, +x2) + 50" :height="Math.max(+y1, +y2) + 50">
    <line 
      :x1="x1" 
      :y1="y1" 
      :x2="x2" 
      :y2="y2" 
      :stroke="color" 
      :stroke-width="width" />
  </svg>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  x1: {
    type: [Number, String],
    default: 100,
  },
  y1: {
    type: [Number, String],
    default: 100,
  },
  x2: {
    type: [Number, String],
    default: 100,
  },
  y2: {
    type: [Number, String],
    default: 100,
  },
  width: {
    type: [Number, String],
    default: 2, // Default width in pixels
  },
  color: {
    type: String,
    default: 'black', // Default color for the stroke
  },
})

</script>

<style scoped>
.cls-1 {
  stroke: var(--neversink-bg-color); /* Optional, can use custom color scheme */
}
</style>
