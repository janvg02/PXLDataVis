<script setup>

import * as d3 from "d3"
import {onMounted} from "vue";

/* Deel 1 Lab
onMounted(async() =>{
  let popData = await d3.csv("population.csv")
  let fertData = await d3.csv("fertility_rate.csv")
  const topCountries = ["Belgium", "China", "Turkiye", "Germany", "Finland", "Niger"]

  popData = popData.filter(r=> topCountries.includes(r["Country Name"]));
  fertData = fertData.filter(r => topCountries.includes((r.Country)))


  for (let i = 0; i < fertData.length; i++){
   const pop = popData.find(r => r["Country Name"] === fertData[i].Country);
    fertData[i].population = +pop["2021"];

    console.log(fertData[i]);
  }
})*/

let axisWidth = 710;
let data = [];
let populationScale = {};
let sliderValue= 1989

onMounted(async() =>{
  let popData = await d3.csv("population.csv")
  let fertData = await d3.csv("fertility_rate.csv")
  const topCountries = ["Belgium", "China", "Turkiye", "Germany", "Finland", "Niger"]

  popData = popData.filter(r=> topCountries.includes(r["Country Name"]));
  fertData = fertData.filter(r => topCountries.includes((r.Country)))


  for (let i = 0; i < fertData.length; i++)
  {
    const pop = popData.find(r => r['Country Name'] === fertData[i].Country);
    fertData[i].population = +pop['2021'];

    for(let j = 1960; j <= 2020; j++)
    {
      fertData[i]['' + j] = +fertData[i]['' + j];
    }
  }
  console.log(fertData)
  data = fertData
  const populationExtents = d3.extent(fertData, d => d.population);
  populationScale = d3.scaleSqrt()
    .domain([0, populationExtents[1]])
    .range([0, 150]);
})


</script>

<template>
  <div >
    <v-app>
      <div id="container">
        <svg width="750" height="500">
          <g v-for="(d, index) in data" :key="index">
            <g :transform="`translate(${20 + d[sliderValue]/8 * axisWidth}, 200)`">
              <circle :r="populationScale(d.population)" />
              <text y="-50" fill="black"> {{d[sliderValue]}} </text>
            </g>
          </g>
          <rect x="20" y="450" :width="axisWidth" height="1" fill="black" />
          <g v-for="n in 9" :key="n">
            <g :transform="`translate(${20 + (n-1) * axisWidth/8}, 440)`">
              <rect x="0" y="0" width="1" height="10" fill="black" />
              <text x="-5" y="-10" fill="black"> {{n - 1}}</text>
            </g>
          </g>
        </svg>
        <div id="slider">
          <v-slider
          label="Jaartal"
          thumb-label="always"
          min="1960"
          max="2020"
          step="1"
          v-model="sliderValue"
          ></v-slider>
        </div>
      </div>
    </v-app>
  </div>
</template>

<style >
#container {
  width: 750px;
}

svg {
  margin: 50px;
}

#slider {
  margin: 50px;
  box-sizing: content-box;
  width: 750px;
}
circle {
  fill: orange;
  opacity: 0.5;
}
</style>
