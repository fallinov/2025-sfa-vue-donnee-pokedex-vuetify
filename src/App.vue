<template>
  <v-app class="bg-grey-lighten-5 pa-0">
    <v-navigation-drawer v-model="drawer" class="pa-0">
      <v-list item-props :items="items" nav />
      <!--      <template #append>
          <v-list-item
            class="ma-2"
            link
            nav
            prepend-icon="mdi-cog-outline"
            title="Settings"
          />
        </template>-->
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
    title: 'Exercice 1',
    subtitle: 'Rendu déclaratif et liaisons d’attributs',
    prependIcon: 'mdi-pencil-outline', // Icône pertinente pour l'exercice
    to: '/',
  },
  {
    title: 'Exercice 2',
    subtitle: 'Rendu déclaratif et liaisons d’attributs',
    prependIcon: 'mdi-pencil-outline', // Icône pertinente pour l'exercice
    to: '/etape2',
  },
]);
</script>
