<template>
  <div :style="{position: 'absolute', height: '100vh', top: top, left: left, width: '15%', textAlign: 'center' }">
    <svg :width="svgWidth" :height="svgHeight" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path
        :d="arrowPath"
        stroke="white"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'MyArrow',
  props: {
    top: {
      type: String,
      required: true
    },
    left: {
      type: String,
      required: true
    },
    x0: {
      type: Number,
      required: true
    },
    y0: {
      type: Number,
      required: true
    },
    x1: {
      type: Number,
      required: true
    },
    y1: {
      type: Number,
      required: true
    }
  },
  computed: {
    // Calculate the path for the arrow based on x0, y0, x1, y1 in percentages
    arrowPath() {
      const x0 = this.x0 * 24 / 100;  // Scale percentage to viewBox scale
      const y0 = this.y0 * 24 / 100;  // Scale percentage to viewBox scale
      const x1 = this.x1 * 24 / 100;  // Scale percentage to viewBox scale
      const y1 = this.y1 * 24 / 100;  // Scale percentage to viewBox scale
      
      // Return the "d" attribute for the arrow path
      return `M${x0} ${y0}L${x1} ${y1}`;
    },
    svgWidth() {
      return '100';  // Width of the SVG, can be customized
    },
    svgHeight() {
      return '100';  // Height of the SVG, can be customized
    }
  }
}
</script>

<style scoped>
/* You can add extra styling here if necessary */
</style>
