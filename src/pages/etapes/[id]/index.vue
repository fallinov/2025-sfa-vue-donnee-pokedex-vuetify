<template>
  <v-container max-width="700">
    <md-content-expansion-panels
      title="Création des pages"
      :source="`${md_souce}/etapes/${id}.md`"
    />
  </v-container>
</template>

<script setup>
// Récupération de l'id de l'étape depuis l'URL
import { useRoute } from 'vue-router';
const route = useRoute();
const id = route.params.id;
// Importe l'url du dépot du fichier .env
const md_souce = import.meta.env.VITE_MD_REPO;
</script>
