<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import {ref, onBeforeMount, watch } from 'vue'
import Tracker from './components/Tracker.vue'
import Map from './components/Map.vue'
import states from 'us-state-converter'
import { store } from './store.js'

const data = ref(undefined)
const center = ref(undefined)
const url = "https://geo.ipify.org/api/v2/country,city?apiKey=at_6yzgJbKKeayaeK9D90fftVlHo9qG6"

async function fetchData(url) {
  const json = await fetch(url).then((r) => r.json())
  data.value = {
    ipAddress: json.ip,
    location: `${json.location.city}, ${states.abbr(json.location.region)} ${json.location.postalCode}`,
    timeZone: json.location.timezone,
    isp: json.isp
  }
  center.value = [json.location.lat, json.location.lng]
}

onBeforeMount(() => {
  fetchData(url)
})
watch(() => 
  store.searchIp,
  (val, oldVal) => {
    fetchData(url + '&ipAddress=' + val)
  }
)
</script>

<template>
  <main class="main">
    <div class="background-img"></div>
    <Map :center="center"></Map>
    <Tracker class="id" :data="data"></Tracker>
  </main>
</template>

<style lang="scss">
@import "./assets/sass/mixins";
@import "./assets/sass/variables";

.background-img {
  background-image: url('./assets/pattern-bg.png');
  background-position: center;
  background-size: cover;
  height: 285px;
  width: 100%;
}

.id {
  position: absolute;
  top: 0;
  width: calc(100% - 2rem);
  margin: 1rem;
  @include breakpoint {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
</style>
