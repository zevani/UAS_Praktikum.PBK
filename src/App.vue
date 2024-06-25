<script setup>
import { ref, computed } from 'vue';
import WeatherPage from './components/WeatherPage.vue';
import MainLayout from './layout/MainLayout.vue';

const options = ["WEATHER", "DAFTAR TUGAS"];
const selectedOption = ref("WEATHER");

const currentComponent = computed(() => {
  if (selectedOption.value === "WEATHER") {
    return WeatherPage;
  } else if (selectedOption.value === "DAFTAR TUGAS") {
    return MainLayout; 
  }
  return null;
});

const selectOption = (option) => {
  selectedOption.value = option;
};
</script>

<template>
  <div id="app">
    <!-- Buttons for selecting options -->
    <div>
      <button
        v-for="option in options"
        :key="option"
        @click="selectOption(option)"
        :class="{ 'active': selectedOption.value === option }"
      >
        {{ option }}
      </button>
    </div>
    
    <!-- Display the selected option -->
    <p>Selected Option: {{ selectedOption.value }}</p>
    
    <!-- Dynamic component rendering based on selectedOption -->
    <component :is="currentComponent"></component>
    
    <!-- Example of directly manipulating an element -->
    <div id="myElement" class="some-class"></div> 
  </div>
</template>

<style>
.active {
  background-color: #007bff;
  color: white;
}
</style>
