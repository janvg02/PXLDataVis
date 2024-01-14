<script setup>
/*
import {onMounted} from "vue";
import Bar from "@/components/Bar.vue";
*/

/* Cursus oef 1
onMounted(() =>{
SayHello();
})
function SayHello(){
  console.log("Hello")
}*/

/* Cursus oef 2
const myArray = [
  {
    animal: 'Cat',
    amount: 100
  },
  {
    animal: 'Dog',
    amount: 30
  },
  {
    animal: 'Pig',
    amount: 60
  },
  {
    animal: 'Cow',
    amount: 80
  }
]*/


/*
import Circle from "@/components/Circle.vue";
*/

import Bar2 from "@/components/Bar2.vue";
const cities = [
  {
    name: 'London',
    population: 8674000
  },
  {
    name: 'New York',
    population: 8406000
  },
  {
    name: 'Sydney',
    population: 4293000
  },
  {
    name: 'Paris',
    population: 2244000
  },
  {
    name: 'Beijing',
    population: 11510000
  }
]
</script>

<template>
<!-- Cursus oef 2
 <svg width=700 height=350>
    <g v-for="(element, index) in myArray" :key="index">
      <Bar :x="index * 30" :height="element.amount" :label="element.animal" />
      </g>
  </svg>-->

<!-- Oefening 1
  <svg width=700 height=350>
    <g v-for="(element, index) in cities" :key="index">
      <Circle :x="index * 100"  :r=element.population/200000 fill="orange" :label="element.name"></Circle>
    </g>
  </svg>-->


  <div class="oef2">
    <svg width="700" height="350">
<!--      <g transform="translate(70, 30)" class="bars">
        <rect height="19" width="346.96000000000004" y="0"></rect>
        <rect height="19" width="336.24" y="20"></rect>
        <rect height="19" width="171.72000000000003" y="40"></rect>
        <rect height="19" width="89.76" y="60"></rect>
        <rect height="19" width="460.40000000000003" y="80">
        </rect>
      </g>
      <g transform="translate(66, 30)" class="labels">
        <text y="13">London</text>
        <text y="33">New York</text>
        <text y="53">Sydney</text>
        <text y="73">Paris</text>
        <text y="93">Beijing</text>
      </g>-->

      <!-- Cursus oef 2
 <svg width=700 height=350>
    <g v-for="(element, index) in myArray" :key="index">
      <Bar :x="index * 30" :height="element.amount" :label="element.animal" />
      </g>
  </svg>-->

      <g v-for="(element, index) in cities" :key="index" >
        <Bar2 class="bars" :y="y" :x="index" :index="element.index" :cy="index * 50" :width="element.population/100000" height="19" :label="element.name" />
      </g>
    </svg>
  </div>
</template>

<style >
.oef2 {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.oef2 body {
  font-family: "Helvetica Neue", Helvetica, sans-serif;
  font-size: 12px;
  color: #3333;
}

.oef2 .bars rect {
  fill: steelblue;
}

.oef2 .bars rect:hover {
  fill: orange;
}

.oef2 .labels text {
  text-anchor: end;
  fill: #fff;
}
</style>
