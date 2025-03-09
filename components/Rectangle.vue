<template>
  <svg class="absolute left-0 top-0">
    <!-- Rectangle -->
    <rect 
      :x="x" 
      :y="y" 
      :width="width" 
      :height="height" 
      :stroke="color" 
      :stroke-width="lineWidth" 
      :fill="fillColor" />
  </svg>
</template>

<script setup>
const props = defineProps({
  x: {
    type: [Number, String],
    default: 50,  // Default x position of the rectangle
  },
  y: {
    type: [Number, String],
    default: 50,  // Default y position of the rectangle
  },
  width: {
    type: [Number, String],
    default: 100,  // Default width of the rectangle
  },
  height: {
    type: [Number, String],
    default: 100,  // Default height of the rectangle
  },
  color: {
    type: String,
    default: 'blue',  // Default stroke (border) color
  },
  fillColor: {
    type: String,
    default: 'transparent',  // Default fill color (transparent by default)
  },
  lineWidth: {
    type: [Number, String],
    default: 2,  // Default width of the rectangle's border
  }
})
</script>

<style scoped>
/* Optional custom styles */
</style>
