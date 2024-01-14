<script setup>
import * as d3 from "d3"
import {onMounted} from "vue";

/* Oefening 1 Lab
onMounted(async() => {
    const data = await d3.csv('harry_potter.csv');
    console.log(data);
})*/

/* Oefening 2 lab
function typeConversion(d)
{
  return {
    genre: d.genre.toLowerCase(),
    budget: +d.budget,
    revenue: +d.revenue
  };
}
function dataLoaded(d){
  return d.filter ( r=> {
   return r.budget > 0 && r.genre && r.revenue > 0
  })
}

onMounted(async() => {
  const data = await d3.csv('movies.csv', typeConversion);
  const filteredMovies = dataLoaded(data)
  console.log(filteredMovies);

})*/

/* Oefening 3 Lab
function typeConversion(d) {
  return {
    genre: d.genre.toLowerCase(),
    budget: +d.budget,
    revenue: +d.revenue
  };
}
function prepareBarChart(d){
  const dataMap = d3.rollup(
      d,
      r => d3.sum(r, x => x.revenue),
      d => d.genre
  )
  const dataArray = Array.from(dataMap, d => ({ genre: d[0], revenue: d[1] }));
  return dataArray;
}
function dataLoaded(d){
  return d.filter ( r=> {
   return r.budget > 0 && r.genre && r.revenue > 0
  })
}

onMounted(async() => {
  const data = await d3.csv('movies.csv', typeConversion);
  const filteredMovies = dataLoaded(data);
  const finishedData = prepareBarChart(filteredMovies)
  console.log(finishedData);
})*/


let movieData = ref([]);

function typeConversion(d) {
  return {
    genre: d.genre.toLowerCase(),
    budget: +d.budget,
    revenue: +d.revenue
  };
}
function prepareBarChart(d){
  const dataMap = d3.rollup(
      d,
      r => d3.sum(r, x => x.revenue),
      d => d.genre
  )
  const dataArray = Array.from(dataMap, d => ({ genre: d[0], revenue: d[1] }));
  return dataArray;
}
function dataLoaded(d){
  return d.filter ( r=> {
   return r.budget > 0 && r.genre && r.revenue > 0
  })
}

onMounted(async() => {
  const data = await d3.csv('movies.csv', typeConversion);
  const filteredMovies = dataLoaded(data);
  const finishedData = prepareBarChart(filteredMovies)
  console.log(finishedData);
})

</script>

<template>

</template>

<style scoped>

</style>
