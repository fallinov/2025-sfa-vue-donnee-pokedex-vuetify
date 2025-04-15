<template>
  <v-container max-width="700">
    <h1>Exercice 8</h1>
    <div class="exe-objectifs">
      <h2>Objectifs</h2>
      <ul>
        <li>Créer un composant enfant <code>PokemonCard</code> qui reçoit les données d'un Pokémon via une <strong>prop</strong>.</li>
        <li>Utiliser un <strong>événement personnalisé</strong> pour permettre au composant enfant de signaler sa suppression au parent.</li>
        <li>Ajouter un champ de formulaire dans le composant parent pour ajouter un Pokémon à la liste.</li>
        <li>Afficher une liste de cartes Pokémon dans le composant parent et permettre leur suppression.</li>
      </ul>
    </div>
    <v-divider class="my-4" />
    <div class="exe-zone">
      <h2>Zone d'exercice</h2>
      <!-- Formulaire pour ajouter un Pokémon -->
      <v-form @submit.prevent="addPokemon" class="mb-4">
        <v-text-field
          v-model="newPokemon"
          label="Ajouter un Pokémon"
          placeholder="Entrez le nom d'un Pokémon"
          outlined
        ></v-text-field>
        <v-btn type="submit" color="primary" class="mt-2">
          Ajouter
        </v-btn>
      </v-form>

      <!-- Liste des Pokémon -->
      <v-card class="mx-auto my-6 pa-2" max-width="500">
        <v-card-title>Liste des Pokémon</v-card-title>
        <v-card-text>
          <v-alert v-if="pokemons.length === 0" type="info">
            La liste est vide.
          </v-alert>
          <v-list v-else>
            <PokemonCard
              v-for="(pokemon, index) in pokemons"
              :key="index"
              :pokemonName="pokemon"
              @remove="removePokemon(index)"
            />
          </v-list>
        </v-card-text>
      </v-card>
    </div>
  </v-container>
</template>

<script setup>
import { ref } from 'vue';
import PokemonCard from "@/components/PokemonCard.vue";

// Liste initiale des Pokémon
const pokemons = ref(["Pikachu", "Bulbizarre", "Salamèche", "Carapuce", "Rondoudou"]);

// Champ de saisie pour un nouveau Pokémon
const newPokemon = ref('');

// Ajouter un Pokémon à la liste
const addPokemon = () => {
  const trimmedPokemon = newPokemon.value.trim();
  if (trimmedPokemon) {
    pokemons.value.push(trimmedPokemon);
    newPokemon.value = ''; // Réinitialise le champ de saisie
  }
};

// Supprimer un Pokémon de la liste
const removePokemon = (index) => {
  pokemons.value.splice(index, 1);
};
</script>
