<script setup>
import {onMounted, ref} from "vue";
import * as d3 from "d3"

let data = ref([])
let albums = ref([]);
let selectedTracks = ref([]);
let selectedAlbum = ref("Taylor Swift");
let yFilters = ref(['Energy', 'Tempo']);
let selectedFilter = ref('Energy');

const width = 750;
const height = 400;

onMounted(async () => {
  const rawData = await d3.csv('taylorswift.csv', filterData);
  console.log(rawData);

  data.value = rawData;
  albums.value = getAlbums(rawData);

  const tempoExtents = d3.extent(rawData, r => r.tempo);
  tempoScale(tempo).domain([0, tempoExtents[1]]).range([0, width]);

  console.log(albums);
});

function filterData(d) {
  return {
    track_name: d.track_name,
    danceability: +d.danceability,
    energy: +d.energy,
    tempo: +d.tempo,
    release: +d.album_release_year,
    album: d.album_name
  }
}

function getAlbums() {
  const filtered = data.value.filter((r, index) => {
    const idx = data.value.findIndex(x => {
      return x.album === r.album
    })
    return idx === index
  })
  return filtered.map(x => x.album);
}

function getY(track) {
  return height - getTrackData(track).danceability * height;
}

function getX(track) {
  if (selectedFilter.value === yFilters.value[0]) {
    console.log("0");
    return width * getTrackData(track).energy;
  } else {

    console.log("1");
    return tempoScale(getTrackData(track).tempo);
  }
}

function getTracks(album) {
  const filtered = data.value.filter(r => {
    return r.album === album
  });
  return filtered.map(x => x.track_name);
}

function getTrackData(track) {
  return data.value.find(x => {
    return x.track_name === track;
  })
}

function selectAllTracks() {
  const allTracks = getTracks(selectedAlbum.value);
  allTracks.forEach((t) => {
    if (!selectedTracks.value.includes(t)) selectedTracks.value.push(t);
  });
}

function deselectAllTracks() {
  const allTracks = getTracks(selectedAlbum.value);
  selectedTracks.value = selectedTracks.value.filter((t) => !allTracks.includes(t));
}
</script>

<template>
  <v-app>
    <v-main>
      <svg :width="width + 300" :height="height + 30">
        <g transform="translate(30, 30)">
          <rect x="0" y="0" :height=height width="2"/>
          <rect x="0" :y="height - 2" height="2" :width=width />
            <g transform="rotate(90)">
              <text y="-10">DANSBAARHEID</text>
            </g>
            <text :x="width - 75" :y="height - 10"> {{ selectedFilter.toUpperCase() }}</text>


        </g>
      </svg>

      <div id="controls">
        <v-container fluid>
          <v-radio-group inline v-model="selectedFilter">
            <v-radio
              v-for="n in yFilters"
              :key="n"
              :label="n"
              :value="n"
            ></v-radio>
          </v-radio-group>
        </v-container>

        <v-container fluid>
          <v-row>
            <v-col>
              <v-select
                label="Album"
                :items="albums"
                v-model="selectedAlbum"
              ></v-select>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <div v-for="(track, index) in getTracks(selectedAlbum)" :key="index">
                <v-checkbox :label="track" :value="track" v-model="selectedTracks"></v-checkbox>
              </div>
            </v-col>
            <v-col>
              <g v-for="track in selectedTracks">
                <g :transform="`translate(${getX(track)}, ${getY(track)})`">
                  <circle r="5"/>
                  <text x="15" y="15"> {{ track }}</text>
                </g>
              </g>
            </v-col>
          </v-row>
          <v-col>
            <v-row>
              <g>
                <v-btn @click="selectAllTracks">Select all tracks</v-btn>
                <v-btn @click="deselectAllTracks">Deselect all tracks</v-btn>
              </g>
            </v-row>
          </v-col>
        </v-container>
      </div>
    </v-main>
  </v-app>
</template>
