<script setup>
import { ref, onBeforeMount } from 'vue'
import Field from './Field.vue';
import SearchBar from './SearchBar.vue';

defineProps({
  data: Object
})
</script>

<template>
  <div v-if="data" class="tracker">
    <h1 class="tracker__title">IP Address Tracker</h1>
    <SearchBar class="tracker__search-bar" placeholder="Search for any IP address or domain"></SearchBar>
    <div class="tracker__card card">
      <Field class="card__field" label="IP Address" v-bind:content="data.ipAddress"></Field>
      <Field class="card__field" label="Location" v-bind:content="data.location"></Field>
      <Field class="card__field" label="Timezone" v-bind:content="'UTC ' + data.timeZone"></Field>
      <Field class="card__field" label="ISP" v-bind:content="data.isp"></Field>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import "../assets/sass/mixins";
@import "../assets/sass/variables";

.tracker {
  &__title {
    font-size: 1.5rem;
    text-align: center;
    color: #fff;
    font-weight: $fw-medium;
    margin-bottom: 1.5rem;
    @include breakpoint {
      margin-top: 1.5rem;
    }
  }
  &__search-bar {
    margin-bottom: 1rem;
    @include breakpoint {
      margin-bottom: 2.5rem;
    }
  }
}
.card {
  padding: 1rem;
  border-radius: 15px;
  background-color: #fff;
  box-shadow: 0 1px 5px $neutral-400;
  @include breakpoint {
    padding: 2rem;
    width: 1100px;
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
  &__field {
    position: relative;
    @include breakpoint {
      width: 25%;
      padding: 0 1.5rem;
      &:first-of-type {
        padding-left: 0;
      }
      &:not(:first-child)::after {
        content: '';
        position: absolute;
        border-right: 1px solid $neutral-400;
        top: .5rem;
        left: 0;
        bottom: .5rem;
      }
    }
    &:not(:last-child) {
      padding-bottom: 1rem;
      @include breakpoint {
        padding-bottom: 0;
      }
    }
  }
}
</style>