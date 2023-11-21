<template>
  <g :transform="`translate(${x}, ${y})`">
    <circle :r="r" fill="yellow" stroke="black" :stroke-width="strokeWidth"></circle>
    <circle :cx="-eyeOffsetX" :cy="-eyeOffsetY" :r="eyeRadius" fill="black"></circle>
    <circle :cx="eyeOffsetX" :cy="-eyeOffsetY" :r="eyeRadius" fill="black"></circle>
  </g>
</template>

<script setup>
defineProps({
  x: {
    type: Number,
    required: true
  },
  y: {
    type: Number,
    required: true
  },
  r: {
    type: Number,
    required: true
  },
  strokeWidth: {
    type: Number,
    required: true
  },
  eyeOffsetX: {
    type: Number,
    required: true
  },
  eyeOffsetY: {
    type: Number,
    required: true
  },
  eyeRadius: {
    type: Number,
    required: true
  }
})
</script>