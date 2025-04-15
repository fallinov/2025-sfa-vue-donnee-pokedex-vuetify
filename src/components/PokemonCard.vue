<template>
  <v-list-item class="d-flex align-center">
    <v-list-item-title>{{ pokemonName }}</v-list-item-title>
    <v-btn icon="mdi-delete" variant="text" @click="$emit('remove')"></v-btn>
  </v-list-item>
</template>

<script setup>
defineProps({
  pokemonName: {
    type: String,
    required: true,
  },
});
</script>

<style scoped>
.v-list-item {
  border-bottom: 1px solid #e0e0e0;
}
</style>
