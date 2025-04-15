## 🎯 Objectifs de l’étape
Dans cette étape, vous allez créer les **quatre pages principales** de l’application : Accueil, Favoris, FAQ, et Monde Pokémon.  
Vous découvrirez comment :
- créer des fichiers `.vue` représentant des pages dans un projet Vue 3,
- structurer une page avec un `<template>` simple,
- et **vérifier le bon fonctionnement du routage automatique** basé sur les fichiers.

## 📁 Créer les fichiers `.vue`
Dans le dossier `src/pages/`, créez les 4 fichiers suivants :
- `index.vue`
- `Favoris.vue`
- `FAQ.vue`
- `KantoMap.vue`

## 🏷️ Ajouter un titre sur chaque page
Dans chaque fichier `.vue`, ajoutez un élément `<template>` contenant un seul titre `<h1>` qui décrit la page.  
Par exemple dans `index.vue` :
```html
<template>
  <h1>Pokédex : page d'accueil</h1>
</template>
```

## 📝 Texte à utiliser pour chaque page
Voici le texte à placer dans chaque balise `<h1>` :

| Fichier        | Contenu du `<h1>`                  |
|----------------|------------------------------------|
| `index.vue`    | Pokédex : page d'accueil           |
| `Favoris.vue`  | Mes Pokémons Favoris               |
| `FAQ.vue`      | Foire Aux Questions (FAQ)          |
| `KantoMap.vue` | Monde Pokémon                      |

## 🔍 Tester les routes dans le navigateur
Lance ton serveur de développement avec `npm run dev`, puis vérifie que chaque page s'affiche correctement aux adresses suivantes :
- `/`
- `/favoris`
- `/faq`
- `/kantomap`

## 🔗 Références utiles
- [📘 Routage basé sur les fichiers – Documentation](https://uvr.esm.is/guide/file-based-routing.html)

## 📦 Solutions

### 🗂️ `src/pages/index.vue`
```html
<!-- src/pages/index.vue -->
<template>
  <h1>Pokédex : page d'accueil</h1>
</template>
```

### 🗂️ `src/pages/Favoris.vue`
```html
<!-- src/pages/Favoris.vue -->
<template>
  <h1>Mes Pokémons Favoris</h1>
</template>
```

### 🗂️ `src/pages/FAQ.vue`
```html
<!-- src/pages/FAQ.vue -->
<template>
  <h1>Foire Aux Questions (FAQ)</h1>
</template>
```

### 🗂️ `src/pages/KantoMap.vue`
```html
<!-- src/pages/KantoMap.vue -->
<template>
  <h1>Monde Pokémon</h1>
</template>
```
