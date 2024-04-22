<script setup>
// Importe le ref de Vue pour créer des variables réactives
  import { ref } from 'vue';
  // Importe BaseInputNumber pour l'utiliser dans le template depuis le script
  import BaseInputNumber from './components/BaseInputNumber.vue';

  // Créer une référence réactive pour la température en Kelvin en SI
  const tempSI = ref(0);

  // Définit un modèle pour Celsius de température pour convertir entre les unités
  const tempCelsius = defineModel('celsius', {
    get: () => tempSI.value - 273.15, // Convertit Kelvin en Celsius via un getter
    set: value => tempSI.value = value + 273.15, // Convertit Celsius en Kelvin via un setter
  });

  // Définit un modèle pour Fahrenheit de température pour convertir entre les unités
  const tempFahrenheit = defineModel('fahrenheit', {
    get: () => tempSI.value * 9 / 5 - 459.67, // Convertit Kelvin en Fahrenheit via un getter
    set: value => tempSI.value = (value + 459.67) * 5 / 9, // Convertit Fahrenheit en Kelvin via un setter
  });

  // Définit un modèle pour Kelvin de température pour convertir entre les unités via direct mapping
  const tempKelvin = defineModel('kelvin', {
    get: () => tempSI.value, // Utilise directement la valeur de tempSI pour Kelvin
    set: value => tempSI.value = value, // Utilise directement la valeur de tempSI pour Kelvin
  });
</script>

<template>
  <!-- Composant input pour la température en Celsius, Fahrenheit et Kelvin -->
  <!-- Chaque input est lié à un modèle de température différent, lié au modèle de conversion en temps réel -->  
  <BaseInputNumber step="0.1" min="-273.15" unit="°C" v-model="tempCelsius"/>
  <BaseInputNumber unit="°F" min="-459.67" v-model="tempFahrenheit"/>
  <BaseInputNumber unit="K" min="0" v-model="tempKelvin"/>
</template>

<style scoped>
  /* Style ... */
  /* BaseInputNumber {
    
  }*/
</style>
