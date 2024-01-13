<script setup>
import Face from './components/Face.vue'
</script>

<template>
<!--  <h1>DataViz</h1>
  <p>Ik vind Vue wel leuk, maar niet zo leuk als Blender.</p>-->
<!--  Oefening 1
<svg width="700" height="350">
    <g v-for="n in 5" :key="n">
    <circle r="20" v-bind:cx="n*100" cy="50" fill="orange"></circle>
    </g>
  </svg>-->

<!-- Oefening 2
  <svg width=1300 height=350>
    <g v-for="n in 3" :key="n">
    <g :transform="`translate(${50 + n *300}, 150)`">
      <circle r=100 fill=yellow stroke="black" stroke-width="10">
      </circle>
      <circle r="10" cx="50" cy="-50" fill="black"></circle>
      <circle r="10" cx="-50" cy="-50" fill="black"></circle>
    </g>
    </g>
  </svg>-->

  <svg width=700 height=350>
    <g v-for="n in 3">
      <Face
          v-bind:x="50 + (n-1) * 100"
          v-bind:y=150
          v-bind:strokeWidth=3
          v-bind:eyeOffsetX=20
          v-bind:eyeOffsetY=10
          v-bind:eyeRadius=8
          v-bind:r=45
      />
    </g>
  </svg>
</template>


