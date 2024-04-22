<script setup>

// importer les fonctions de Vue pour créer des variables réactives
  import { ref, watch, computed } from 'vue';
// importer les composants pour les utiliser dans le template depuis le script
  import TheHeader from './components/TheHeader.vue'; // composant vue pour l'en-tête
  import TheNav from './components/TheNav.vue'; // composant vue pour la navigation
  import AppSchedule from './AppSchedule.vue'; // composant vue pour l'app horaire
  import AppTemperature from './AppTemperature.vue'; // composant vue pour l'app température

  // Définit les routes URL hash paths pour les composants
  const routes = {
    '#schedule': AppSchedule,
    '#temperature': AppTemperature,
  }

  // Référence réactive pour le chemin de l'URL hash
  const currentPath = ref(window.location.hash);

  // Ecoute les changements de l'URL hash pour mettre à jour le chemin actuel
  window.addEventListener('hashchange', () => {
    currentPath.value = window.location.hash;
  })

  // Propriété calculée pour obtenir le composant actuel basé sur le chemin de l'URL hash de manière réactive/dynamique
  const currentView = computed(() => {
    return routes[currentPath.value] ?? AppTemperature; // Par défaut, affiche l'app température si le chemin n'est pas trouvé
  })

</script>

<template>
    <!-- Composants pour l'en-tête, la navigation et le composant actuel basé sur l'URL hash -->
  <TheHeader />
  <TheNav />
  <!-- Composant dynamique basé sur le chemin de l'URL hash -->
  <component :is="currentView" />
</template>

<style scoped>
    /* Style ... */
    /* TheHeader {
        
    }
    TheNav {
        
    }
    component {
        
    } */

</style>