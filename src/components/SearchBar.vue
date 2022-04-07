<script setup>
import {ref} from 'vue'
import { store } from '../store.js'

defineProps({
  placeholder: String
})

const ip = ref("")
</script>

<template>
  <div class="search-bar">
    <input class="search-bar__input" type="text" :placeholder="placeholder" v-model="ip"> 
    <button class="search-bar__button" @click="store.setNewIp(ip)">
      <img src="../assets/icon-arrow.svg" alt="">
    </button>
  </div>
</template>

<style lang="scss">
@import "@/assets/sass/mixins";
@import "@/assets/sass/variables";

.search-bar {
  display: flex;
  flex-direction: row;
  @include breakpoint {
    width: 550px;
  }
  &__input {
    padding: 1rem;
    border-top-left-radius: 15px;
    border-bottom-left-radius: 15px;
    border: none;
    font-weight: $fw-regular;
    width: 100%;
    font-size: 1rem;
    font-family: $font-family;
    &:hover {
      cursor: pointer;
    }
    &:focus-visible {
      outline: none;
    }
  }
  &__button {
    padding: 1rem;
    background-color: $neutral-700;
    border: none;
    width: 3.5rem;
    border-top-right-radius: 15px;
    border-bottom-right-radius: 15px;
    &:hover {
      cursor: pointer;
    }
  }
}
</style>