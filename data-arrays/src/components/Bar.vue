<script setup>
defineProps({
  height: {
    type: Number,
    required: true
  }
})
</script>

<template>
  <g>
  <rect width=20 :height=d.value fill=orange />
  <text x="5" y="110" fill="orange" transform="rotate(50, 5, 110)">{{d.category}}</text>
  </g>
</template>

<style scoped>

</style>