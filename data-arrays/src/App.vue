<script setup>
import { onMounted } from 'vue';
import Bar from './components/Bar.vue';

console.log('Hello');
const data = [
  {
    category: 'Cat',
    value: 10
  },
  {
    category: 'Dog',
    value: 15
  },
  {
    category: 'Pig',
    value: 35
  },
  {
    category: 'Cow',
    value: 25
  }
]
onMounted(() => {
  console.log("Hello from App.vue");
})

function Awesome(){
  console.log("Blender is awesome")
}
</script>

<template>
  <svg width=700 height=175>
    <g v-for="(d, index) in data" :transform="`translate(${index * 30},0)`">
      <Bar :height = d.value></Bar>
    </g>
  </svg>
</template>

<style scoped>


</style>
