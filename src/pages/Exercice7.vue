<template>
  <v-container max-width="700">
    <h1>Exercice 7</h1>
    <div class="exe-objectifs">
      <h2>Objectifs</h2>
      <ul>
        <li>Découvrir et utiliser les hooks du <strong>cycle de vie</strong> dans Vue.js.</li>
        <li>Utiliser <code>onMounted</code> pour exécuter une action lorsque le composant est monté.</li>
        <li>Utiliser <code>onUpdated</code> pour détecter une mise à jour globale du composant.</li>
        <li>Utiliser <code>onUnmounted</code> pour nettoyer des actions, comme annuler un intervalle.</li>
      </ul>
    </div>
    <v-divider class="my-4" />
    <div class="exe-zone">
      <h2>Zone d'exercice</h2>
      <v-card class="mx-auto my-6 pa-2" max-width="500">
        <v-card-title>Cycle de vie de Vue.js</v-card-title>
        <v-card-text>
          <p>Compteur : <strong>{{ counter }}</strong></p>
          <p>Dernière mise à jour : {{ updatedTimestamp }}</p>
          <v-btn color="primary" @click="incrementCounter">Incrémenter</v-btn>
        </v-card-text>
      </v-card>
    </div>
  </v-container>
</template>

<script setup>
import { ref, onMounted, onUpdated, onUnmounted } from 'vue';

// Variables réactives
const counter = ref(0);
const updatedTimestamp = ref('');
let intervalId = null;

// Hook exécuté lorsque le composant est monté
onMounted(() => {
  console.log('Composant monté !');
  // Simule un intervalle qui met à jour le compteur automatiquement
  intervalId = setInterval(() => {
    counter.value++;
  }, 2000);
});

// Hook exécuté lorsque le composant est mis à jour (DOM mis à jour)
onUpdated(() => {
  console.log('Le composant a été mis à jour !');
  const now = new Date();
  updatedTimestamp.value = `${now.toLocaleTimeString()}`;
});

// Hook exécuté lorsque le composant est démonté
onUnmounted(() => {
  console.log('Composant démonté !');
  // Nettoie l'intervalle pour éviter une fuite de mémoire
  clearInterval(intervalId);
});

// Fonction pour incrémenter manuellement le compteur
const incrementCounter = () => {
  counter.value++;
};
</script>

<style scoped>
.exe-objectifs {
  background-color: #f5f5f5;
  padding: 16px;
  border-radius: 8px;
}

.exe-zone {
  margin-top: 16px;
}
</style>
