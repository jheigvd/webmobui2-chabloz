<script setup>
  import { ref } from 'vue';
  import { round } from './utils/math.js';
  const temperatureSi = ref(0);

  const temperatureKelvin = defineModel('kelvin', {
    get() {
      return round(temperatureSi.value);
    },
    set(value) {
      temperatureSi.value = value;
    }
  });

  const temperatureCelsius = defineModel('celsius',{
    get() {
      return round(temperatureSi.value - 273.15);
    },
    set(value) {
      temperatureSi.value = value + 273.15;
    }
  });

  const temperatureFarhenheit = defineModel('farhenheit', {
    get() {
      return round((temperatureSi.value - 273.15) * 9/5 + 32);
    },
    set(value) {
      temperatureSi.value = (value - 32) * 5/9 + 273.15;
    }
  });
</script>

<template>
  <h1>Temperature</h1>
  <div class="grid">
      <input v-model="temperatureKelvin" type="number" name="Kelvin" step="any">
      <span>K</span>

      <input v-model="temperatureCelsius" type="number" name="Celsius">
      <span>°C</span>

      <input v-model="temperatureFarhenheit" type="number" name="Farhenheit">
      <span>°F</span>
  </div>
</template>

<style scoped>
  * {
    box-sizing: border-box;
  }
  h1 {
    text-align: center;
  }
  .grid {
    display: grid;
    place-items: center;
    gap: 1rem 0.3rem;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
  }
  input {
    display: inline-block;
    border: solid black 1px;
    padding: 0.3rem;
    justify-self: end;
    width: 6rem;
  }
  span {
    display: inline-block;
    min-width: 2rem;
    font-weight: bold;
    justify-self: start;
  }
</style>
