<script setup>
  // Importe la fonction `round` depuis un fichier utilitaire local.

  import { round } from '../utils/math.js';
    // Définit les props du composant, avec leurs types, nécessités et valeurs par défaut.
const props = defineProps({
    unit: { // Définit une prop `unit` pour spécifier l'unité de mesure (optionnelle).
      type: String,
      required: false, // Non requis.
      default: false, // Fausse par défaut, signifiant qu'aucune unité n'est spécifiée.
    },
    },
    decimalPlaces: { // Définit une prop `decimalPlaces` pour le nombre de décimales.
      type: Number,
      required: false, // Non requis.
      default: 2, // Par défaut, arrondit à 2 décimales.
    },
  });
  // Définit un modèle pour le composant, utilisant un getter personnalisé.

  const model = defineModel({
    get() {
            // Renvoie la valeur modélisée arrondie selon le nombre de décimales spécifié.

      return round(props.modelValue, props.decimalPlaces);
    }
    // Note: Il n'y a pas de setter, ce qui implique que le modèle est en lecture seule ou
    // qu'il est mis à jour d'une autre manière non montrée ici.
  });
</script>

<template>
  <div>
    <input type="number" v-model="model" v-bind="$attrs">
    <span v-if="unit">{{ unit }}</span>
  </div>
</template>

<style scoped>
  input {
    display: inline-block;
    margin: 0.5rem 1rem;
  }
</style>