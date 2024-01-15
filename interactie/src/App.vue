<script setup>
import * as d3 from "d3"
import {onMounted} from "vue";

onMounted(async() => {
  const rawData = await d3.csv('taylorswift.csv', Data);
  console.log(rawData)
})
function Data(d)
{
  return {
    track_name: d.track_name,
    danceability: +d.danceability,
    energy: +d.energy,
    tempo: +d.tempo,
    album_name: +d.album_name,
    album_release_year: +d.album_release_year,
    data : +[],
    albums: +getAlbums(),
    selectedTracks : +[],
    selectedAlbum: +"Taylor Swift",
    yFilters: +['Energy', 'Tempo'],
    selectedFilter: +'Energy'
  };
}

function getAlbums(){
  const filtered = this.data.filter((r,index)=>{
    const idx = this.data.findIndex(x =>{
      return x.album === r.album
    });
    return idx ===index
  });
  return filtered.map(x => x.album)
}

</script>

<template>

</template>

<style scoped>

</style>
