<template>
  <v-container max-width="700">
    <md-content-expansion-panels
      title="Création des pages"
      :source="`/etapes/${id}.md`"
    />
  </v-container>
</template>

<script setup>
// Récupération de l'id de l'étape depuis l'URL
import { useRoute } from 'vue-router';
const route = useRoute();
const id = route.params.id;
</script>
