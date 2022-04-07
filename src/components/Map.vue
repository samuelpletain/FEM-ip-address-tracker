<script setup>
import { onMounted, onBeforeMount, ref } from 'vue'
import "leaflet/dist/leaflet.css"
import { LMap, LTileLayer, LMarker, LIcon } from '@vue-leaflet/vue-leaflet'
import image from '@/assets/icon-location.svg'


defineProps({
  center: Array,
})

const url = ref('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}')
const attribution = ref('Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>')
const zoom = ref(18)
const maxZoom = ref(18)
const tileSize = ref(512)
const dinamycSize = ref([46, 56])
const options = ref({    
    id: 'mapbox/streets-v11',
    zoomOffset: -1,
    username: 'samuelpletain',
    accessToken: 'pk.eyJ1Ijoic2FtdWVscGxldGFpbiIsImEiOiJjbDFndGdjenEwcmE3M2pwMzdpODRxMHRvIn0.BdVbnMmm2VMN2fd2lSqX9g'
  })
const mapOptions = ref({
  dragging: false,
  zoomControl: false,
  scrollWheelZoom: false})
</script>

<template>
  <l-map style="min-height: 515px; height: calc(100vh - 285px);" :zoom="zoom" :center="center" :max-zoom="maxZoom" :options="mapOptions" v-if="center" id="map">
    <l-tile-layer :url="url" :attribution="attribution" :options="options" :tile-size="tileSize"></l-tile-layer>
    <l-marker v-if="center" :lat-lng="center">
      <l-icon :iconSize="dinamycSize" :icon-url="image"></l-icon>
    </l-marker>
  </l-map>
</template>

<style lang="scss" scoped>
@import "../assets/sass/mixins";
@import "../assets/sass/variables";

#map {
  width: 100%;
  z-index: -1;
  position: relative;
  height: 100vh;
  @include breakpoint {
    height: calc(100vh - 285px);
  }
}
</style>