<template>
  <v-container max-width="700">
    <!-- Donnée de l'exercice -->
    <exercice-objectifs number="5" />
    <!-- Zone de travail pour l'exercice -->
    <div class="exe-zone">
      <h2>Zone d'exercice</h2>
      <v-card class="mx-auto my-6 pa-2" max-width="500">
        <v-card-title>Saisie surveillée</v-card-title>

        <v-card-text>
          <v-alert
            v-if="containsPokemon"
            type="success"
            class="mb-2"
          >
            Vous avez mentionné "Pokémon" !
          </v-alert>

          <v-text-field
            v-model="userInput"
            label="Tapez quelque chose"
            placeholder="Essayez d'écrire Pokémon"
            outlined
          />

          <v-card-subtitle>
            Nombre de caractères :
            {{ userInput.length }}
          </v-card-subtitle>
        </v-card-text>
      </v-card>
    </div>
  </v-container>
</template>

<script setup>
// Importation du composant contenant la donnée de l'exerciced
import ExerciceObjectifs from "@/components/ExerciceObjectifs.vue";

// Importation de la fonction réactive ref
import { ref, watch } from 'vue';

// Variable réactive pour la saisie utilisateur
const userInput = ref('');

// Longueur maximale autorisée
const MAX_LENGTH = 20;

// Variable réactive pour indiquer si "Pokémon" est présent
const containsPokemon = ref(false);

// Watcher pour surveiller la saisie utilisateur
watch(userInput, (newValue) => {
  // Vérifie si "Pokémon" est mentionné
  containsPokemon.value = newValue.toLowerCase().includes('pokémon');

  // Réinitialise la saisie si elle dépasse la longueur maximale
  if (newValue.length > MAX_LENGTH) {
    userInput.value = '';
  }
});
</script>
