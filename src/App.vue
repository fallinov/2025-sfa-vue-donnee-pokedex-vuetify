<template>
  <v-app class="bg-grey-lighten-5 pa-0">
    <v-navigation-drawer v-model="drawer" class="pa-0">
      <v-list nav>
        <v-list-item
          v-for="item in items"
          :key="item.value"
          :subtitle="item.subtitle"
          :title="item.title"
          :prepend-icon="item.icon"
          @click="page = item.link"
        />
      </v-list>
    </v-navigation-drawer>

    <v-app-bar border="b" class="ps-4" flat>
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <v-app-bar-title>Exercice Pokédex Vuetify</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <v-container max-width="700">
        <md-content-expansion-panels
          title="Création des pages"
          :source="`${md_souce}/${page}`"
        />
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const page = ref('/etapes/2.md')


const drawer = ref(true)
const items = ref([
  {
    title: 'Introduction',
    subtitle: 'Présentation & mise en place',
    icon: 'mdi-flag-checkered',
    link: '/index.md',
  },
  {
    title: ' Étape 1',
    subtitle: 'Créer les pages',
    icon: 'mdi-book-open-page-variant-outline',
    link: '/etapes/1.md',
  },
  {
    title: 'Étape 2',
    subtitle: 'Ajouter les liens de menu',
    icon: 'mdi-link-variant-plus',
    link: '/etapes/2.md',
  },
  {
    title: 'Étape 3',
    subtitle: 'Page Monde Pokémon',
    icon: 'mdi-earth-box',
    link: '/etape3',
  },
  {
    title: 'Étape 4',
    subtitle: 'Page FAQ',
    icon: 'mdi-frequently-asked-questions',
    link: '/etape4',
  },
  {
    title: 'Étape 5',
    subtitle: 'Pokémons en colonnes',
    icon: 'mdi-view-column',
    link: '/etape5',
  },
]);

// Récupération de l'id de l'étape depuis l'URL

// Importe l'url du dépot du fichier .env
const md_souce = import.meta.env.VITE_MD_REPO;
</script>
