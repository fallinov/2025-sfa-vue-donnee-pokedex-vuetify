<template>
  <h1 class="mb-4">Exercice {{ props.number }}</h1>
  <v-expansion-panels class="mb-6" variant="accordion">
    <v-expansion-panel
      v-for="(section, index) in sections"
      :key="index"
    >
      <v-expansion-panel-title>
        <span v-html="section.title"/>
      </v-expansion-panel-title>
      <v-expansion-panel-text>
        <div v-html="section.content"/>
      </v-expansion-panel-text>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<script setup>
import {ref, onMounted, computed} from 'vue';
import MarkdownIt from 'markdown-it';

let props = defineProps({number: String});

// Initialisation de MarkdownIt
const markdown = new MarkdownIt();
const source = ref('');

// Import dynamique du fichier Markdown
onMounted(async () => {
  try {
    const response = await fetch(`./exercices/${props.number}.md`);
    if (!response.ok) throw new Error('Erreur de chargement du fichier');
    source.value = await response.text();
  } catch (error) {
    console.error('Erreur de chargement du contenu Markdown :', error);
    source.value = '# Erreur de chargement du contenu Markdown';
  }
});

// Transformation du Markdown en sections d'accordéon
const sections = computed(() => {
  const lines = source.value.split('\n');
  const sections = [];
  let currentSection = null;

  lines.forEach((line) => {
    if (line.startsWith('## ')) {
      if (currentSection) {
        sections.push(currentSection);
      }
      currentSection = {
        title: markdown.render(line),
        content: '',
      };
    } else if (currentSection) {
      currentSection.content += markdown.render(line);
    }
  });

  if (currentSection) {
    sections.push(currentSection);
  }

  return sections;
});
</script>

<style scoped lang="sass">
.v-expansion-panel-title
  :deep(h2)
       font-size: 1.125rem

.v-expansion-panel-text
  :deep(ul)
    padding: 0
    padding-left: 1.5rem
    margin: 0

    li
      padding: .25em 0
      margin: 0

</style>
