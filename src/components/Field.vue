<script setup>
import { ref } from 'vue';

defineProps({
  label: String,
  content: String
})
</script>

<template>
  <div class="field">
    <h2 class="field__label">{{ label }}</h2>
    <p class="field__content">{{ content }} </p>
  </div>
</template>

<style scoped lang="scss">
@import "../assets/sass/mixins";
@import "../assets/sass/variables";
.field {
  text-align: center;
  font-weight: $fw-medium;
  @include breakpoint {
    text-align: left;
  }
  &__label {
    color: $neutral-400;
    font-size: .5rem;
    text-transform: uppercase;
    letter-spacing: .1rem;
    @include breakpoint {
      font-size: .7rem;
      padding-bottom: .5rem;
    }
  }
  &__content {
    font-size: 1rem;
    padding: .5rem;
    @include breakpoint {
      padding: 0;
      font-size: 1.5rem;
    }
  }
}
</style>