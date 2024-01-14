<script setup>
defineProps({
  y:{
    type:Number,
    required: true
  },
  x:{
    type:Number,
    required: true
  },
  label:{
    type: String,
    required:true
  },
  width:{
    type:Number,
    required:true
  }




})
</script>

<template>
  <g  :transform="`translate(${x}, ${y})`">
    <rect height="19" :width fill=orange />
    <text class="labels"  fill="orange" > {{ label }}</text>
  </g>
</template>

<style scoped>

</style>