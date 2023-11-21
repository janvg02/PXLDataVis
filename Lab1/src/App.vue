<script setup>
import Face from "@/components/Face.vue";
</script>

<template>
  <div id="app">
    <svg width="700" height="350">
      <g v-for="n in 3" :key="n">
        <Face
            :x="50 + (n-1) * 100"
            y="150"
            :stroke-width="3"
            :eyeOffsetX="20"
            :eyeOffsetY="10"
            :eyeRadius="8"
            :r="45"
        />
      </g>
    </svg>
  </div>
</template>

<style scoped>

</style>
