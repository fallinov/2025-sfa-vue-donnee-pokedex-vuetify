## 🎯 Objectifs de l'étape
Dans cette étape, vous allez **compléter la barre de navigation** située en haut de l’application pour permettre aux utilisateurs de naviguer facilement entre les différentes pages.  
Vous apprendrez à :
- localiser et modifier une structure de menu dynamique (`menuItems`),
- utiliser la directive `v-for` pour générer des boutons automatiquement,
- et associer à chaque page une **icône Material Design** pertinente.


## 🧩 Localiser le tableau `menuItems`
Ouvre le fichier `src/components/AppHeader.vue` et localise la section `<script setup>`.

Cherche la constante `menuItems` qui ressemble à ceci :

```js
const menuItems = [
  { title: 'Accueil', path: '/', icon: 'mdi-pokeball' },
]
```

## ➕ Ajouter les liens vers les autres pages
Ajoute les trois éléments suivants au tableau `menuItems` :

```js
{ title: 'Favoris', path: '/favoris', icon: 'mdi-heart' },
{ title: 'FAQ', path: '/faq', icon: 'mdi-help-circle' },
{ title: 'Monde Pokémon', path: '/kantomap', icon: 'mdi-map' },
```

Tu obtiendras un tableau `menuItems` contenant les 4 pages :

```js
const menuItems = [
  { title: 'Accueil', path: '/', icon: 'mdi-pokeball' },
  { title: 'Favoris', path: '/favoris', icon: 'mdi-heart' },
  { title: 'FAQ', path: '/faq', icon: 'mdi-help-circle' },
  { title: 'Monde Pokémon', path: '/kantomap', icon: 'mdi-map' },
]
```

## 🎨 Choisir les bonnes icônes
Utilise les **Material Design Icons** disponibles sur ce site :
👉 [https://pictogrammers.com/library/mdi](https://pictogrammers.com/library/mdi)

N’oublie pas d’ajouter le préfixe `mdi-` devant chaque nom d’icône.

## 📐 Résultat attendu dans le menu
Une **barre de navigation Vuetify (`v-app-bar`)** contenant :
- un logo à gauche (via `v-avatar`)
- le titre "Pokédex"
- une série de boutons générés dynamiquement par `v-for`, un pour chaque entrée de `menuItems`

## 📦 Solutions

### 🗂️ `src/components/AppHeader.vue`
```html
<!-- src/components/AppHeader.vue -->
<script setup>
const menuItems = [
  { title: 'Accueil', path: '/', icon: 'mdi-pokeball' },
  { title: 'Favoris', path: '/favoris', icon: 'mdi-heart' },
  { title: 'FAQ', path: '/faq', icon: 'mdi-help-circle' },
  { title: 'Monde Pokémon', path: '/kantomap', icon: 'mdi-map' },
]
</script>

<template>
  <v-app-bar app>
    <v-avatar class="ma-2" color="red" @click="$router.push('/')">
      <v-icon>mdi-pokeball</v-icon>
    </v-avatar>

    <v-toolbar-title>Pokédex</v-toolbar-title>

    <v-spacer />

    <v-btn
      v-for="item in menuItems"
      :key="item.path"
      :to="item.path"
      variant="text"
      class="text-capitalize"
    >
      <v-icon start>{{ item.icon }}</v-icon>
      {{ item.title }}
    </v-btn>
  </v-app-bar>
</template>
```


