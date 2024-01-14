<script setup>
/*Oefening 1*/
defineProps({
  r: {
    type: Number,
    required: true
  },
  x: {
    type:Number,
    required: true
  },
  label: {
    type: String,
    required: true
  }
})
</script>

<template>
  <g :transform="`translate(${x+200}, ${200-r})`">
    <circle :r=r :x="x" fill=red :label="label">
    </circle>
    <text :x="1"  fill="blue"> {{ label }}</text>
  </g>
</template>

<style scoped>

</style>