<template>
  <v-app class="bg-grey-lighten-5 pa-0">
    <v-navigation-drawer v-model="drawer" class="pa-0">
      <v-list item-props :items="items" nav />
    </v-navigation-drawer>

    <v-app-bar border="b" class="ps-4" flat>
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <v-app-bar-title>Exercice Pokédex Vuetify</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <router-view  />
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const drawer = ref(true)

const items = ref([
  {
    title: 'Introduction',
    subtitle: 'Présentation & mise en place',
    prependIcon: 'mdi-flag-checkered',
    to: '/',
  },
  {
    title: ' Étape 1',
    subtitle: 'Créer les pages',
    prependIcon: 'mdi-book-open-page-variant-outline',
    to: '/etape1',
  },
  {
    title: 'Étape 2',
    subtitle: 'Ajouter les liens de menu',
    prependIcon: 'mdi-link-variant-plus',
    to: '/etape2',
  },
  {
    title: 'Étape 3',
    subtitle: 'Page Monde Pokémon',
    prependIcon: 'mdi-earth-box',
    to: '/etape3',
  },
  {
    title: 'Étape 4',
    subtitle: 'Page FAQ',
    prependIcon: 'mdi-frequently-asked-questions',
    to: '/etape4',
  },
  {
    title: 'Étape 5',
    subtitle: 'Pokémons en colonnes',
    prependIcon: 'mdi-view-column',
    to: '/etape5',
  },
]);
</script>
