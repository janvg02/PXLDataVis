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


/* oef 2 oefeningen
function typeConversion(d)
{
  return {
    title: d.title.toLowerCase(),
    vote_average: +d.vote_average,
    vote_count: +d.vote_count,
    homepage: +d.homepage,
  };
}
function dataLoaded(d){
  return d.filter ( r=> {
    return r.title  && r.vote_average && r.vote_count > 1000 ;
  })
}

onMounted(async() => {
  const data = await d3.csv('movies.csv', typeConversion);
  const filteredMovies = dataLoaded(data)
  console.log(filteredMovies);
})*/

/*Oef 3 oefeningen
function typeConversion(d)
{
  const date = d3.timeParse('%Y-%m-%d');
  const countries = JSON.parse(d.production_countries );
  return {
    title: d.title.toLowerCase(),
    production_countries: countries,
    release_date: +date(d.release_date)
  };
}
function dataLoaded(d){
  return d.filter ( r=> {
    return r.title && r.production_countries && r.release_date ;
  })
}

onMounted(async() => {
  const data = await d3.csv('movies.csv', typeConversion);
  const filteredMovies = dataLoaded(data)
  console.log(filteredMovies);
})*/


/* Oef 4 oefeningen
onMounted(async () => {
  const data = await d3.csv('abonnees_genk.csv', typeConversion);
  const filteredCode = dataLoaded(data);
  const groupedData = groupByPostcode(filteredCode);
  const filteredGroupedData = filterGroupedData(groupedData);
  console.log(filteredGroupedData);
});

function typeConversion(d) {
  const PostcodeNumber = parseInt(d.Postcode);
  return {
    Postcode: PostcodeNumber
  };
}

function dataLoaded(d) {
  return d.filter(r => {
    return r.Postcode && String(r.Postcode).length === 4;
  });
}

function groupByPostcode(data) {
  return d3.rollup(
      data,
      v => v.length,
      d => d.Postcode
  );
}

function filterGroupedData(groupedData) {
  return Array.from(groupedData, d => ({ Postcode: d[0], AantalAbonnees: d[1] }))
      .sort((a, b) => b.AantalAbonnees - a.AantalAbonnees);
}*/
</script>

<template>
<!-- oefening 3 Lab + oef 1 oefeningen
  <svg width=700 height=350>
    <g v-for="(m, index) in movieData">
      <g :transform="`translate(${index * 55}, ${305 - xScale(m.revenue)})`">
        <rect :width="20" :height=xScale(m.revenue) fill=orange />
        <text transform="rotate(10,0,20)" text-anchor="middle" fill="white">{{ m.genre }}</text>
      </g>
    </g>
  </svg>-->
</template>

<style scoped>

</style>
