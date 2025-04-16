# 📕 Exercice Pokédex Vuetify
![screeshot-final.png](public/screeshot-final.png)
## 🧭 Introduction

Dans cet exercice, vous allez créer un **Pokédex interactif** avec **Vue.js**, **Vuetify** et **Pinia**.

L’objectif est d’apprendre à développer une application web moderne avec un framework JavaScript puissant (Vue 3) et une bibliothèque de composants (Vuetify 3) qui permet de construire des interfaces élégantes rapidement.

Vous allez découvrir comment :

- concevoir plusieurs pages avec un **routage automatique**,
- utiliser **Pinia** pour partager des données entre vos composants,
- structurer une application **modulaire et évolutive**,
- afficher dynamiquement des données sous forme de **composants réutilisables**,
- enrichir l’expérience utilisateur avec des **animations**, des **boîtes de dialogue**, et des **icônes bien choisies** (promis, pas que des cœurs et des Pokéballs 🥲).

> 🔐 Une **fonctionnalité d’authentification** sera ajoutée plus tard dans l'exercice. Elle permettra aux utilisateurs connectés d’ajouter ou de supprimer des Pokémon.

**Pages à réaliser** :

L'application contiendra les pages suivantes, que vous allez progressivement construire :

- 🏠 **Accueil** : liste des Pokémon avec barre de recherche
- ❤️ **Favoris** : liste des Pokémon ajoutés aux favoris
- ❓ **FAQ** : liste de questions/réponses repliables
- 🗺️ **Monde Pokémon** : carte du monde + texte descriptif
- 🔐 **Connexion (plus tard)** : permet d’ajouter ou supprimer des Pokémon

Exemple de solution : [https://kode.ch/pokedex](https://kode.ch/pokedex)

## ⚙️ Mise en place

### Installer les dépendances

Ouvrez un terminal à la racine du projet et exécutez la commande suivante :

```bash
npm install
```

### Lancer le serveur de développement

Une fois les dépendances installées, démarrez le serveur avec :

```bash
npm run dev
```

### Accéder à l'application dans le navigateur

Ouvrez l'URL affichée dans le terminal (en général [http://localhost:3000](http://localhost:3000)) pour afficher l'application de départ.

Vous devriez apercevoir le résultat suivant :

![screeshot-start.png](public/screeshot-start.png)
---

## 📁 Structure du projet

Voici une vue d'ensemble des différents dossiers et fichiers du projet.

### `public/`

Contient le fichier `index.html`, qui est le point d'entrée statique de l'application.

- `images/` : Contient les images des Pokémons accessibles via des chemins publics (`/images/…`).

### `src/`

Le dossier principal qui contient tout le code source de l'application :

- `assets/` : Contient les ressources statiques comme les images, les icônes, le logo du site, etc.
- `components/` : Composants Vue réutilisables (cartes, puces, header, etc.). Ils sont auto-importés grâce au plugin `unplugin-vue-components`.
- `pages/` : Contient les différentes vues de l'application. Chaque fichier `.vue` correspond automatiquement à une route grâce à `unplugin-vue-router`.
    - `index.vue` : Page d’accueil principale.
    - `[...path].vue` : Page 404 affichée si aucune route ne correspond.
- `stores/` : Gestion d’état avec **Pinia**.
    - `pokemons.js` : Gère la liste, les types et les favoris des Pokémon.
    - `authStore.js` : Simule un système d’authentification locale.
- `plugins/` : Initialisation de Vuetify, Pinia et Vue Router. Le fichier `index.js` centralise l’enregistrement des plugins, `vuetify.js` contient la config Vuetify.
- `styles/` : Fichier `settings.scss` contenant les personnalisations SCSS pour Vuetify et les animations CSS.
- `utils/` : Fonctions utilitaires comme `getImageUrl()` pour construire des chemins d’image.
- `typed-router.d.ts` : Fichier généré automatiquement pour typer les routes (utile si vous activez TypeScript).
- `App.vue` : Composant racine affichant la structure globale de l’application.
- `main.js` : Point d’entrée de l’application. Crée l’app Vue et enregistre les plugins (router, pinia, vuetify).

### 🧩 Affichage (layout) de base

Le composant principal `App.vue` est composé de trois sections principales :

- `<app-header>` : Charge le composant `components/AppHeader.vue` qui contient l’en-tête du site (logo et menu de navigation).
- `<v-main>` : Contenu principal qui contient le composant `<router-view>`, utilisé pour afficher dynamiquement la page active selon la route.
- `<v-footer>` : Pied de page contenant une ligne simple (ex : date ou nom du projet).

### Fichier de configuration

- `vite.config.mjs` : Configuration Vite : plugins (vuetify, auto-import, layouts...), alias, port local, etc.&#x20;
