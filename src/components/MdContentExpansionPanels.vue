<template>
  <h1 class="mb-4">{{ title }}</h1>
  <v-expansion-panels class="mb-6" variant="accordion">
    <v-expansion-panel
      v-for="(section, index) in sections"
      :key="index"
    >
      <v-expansion-panel-title>
        <span v-html="section.title" />
      </v-expansion-panel-title>
      <v-expansion-panel-text>
        <div v-html="section.content" class="markdown-content" />
      </v-expansion-panel-text>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import MarkdownIt from 'markdown-it';
import hljs from 'highlight.js';
import 'highlight.js/styles/atom-one-dark.css'; // Tu peux changer le thème si tu veux

// Définition des props
const props = defineProps({
  source: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    default: 'Documentation',
  },
});

// Initialisation de MarkdownIt avec coloration syntaxique
const markdown = new MarkdownIt({
  html: true,
  linkify: true,
  highlight: function (str, lang) {
    if (lang && hljs.getLanguage(lang)) {
      try {
        return `<pre class="hljs"><code>${hljs.highlight(str, { language: lang }).value}</code></pre>`;
      } catch (__) {}
    }
    return `<pre class="hljs"><code>${markdown.utils.escapeHtml(str)}</code></pre>`;
  }
});

const contenuMarkdown = ref('');

// Chargement dynamique du fichier Markdown
onMounted(async () => {
  if (!props.source) {
    console.error('Aucun fichier source spécifié');
    return;
  }

  try {
    const response = await fetch(props.source);
    if (!response.ok) throw new Error('Erreur de chargement du fichier');
    contenuMarkdown.value = await response.text();
  } catch (error) {
    console.error('Erreur de chargement du contenu Markdown :', error);
    contenuMarkdown.value = '# Erreur de chargement du contenu Markdown';
  }
});

// Découpage du fichier en sections
const sections = computed(() => {
  const lines = contenuMarkdown.value.split('\n');
  const sections = [];
  let currentSection = null;

  lines.forEach((line) => {
    if (line.startsWith('## ')) {
      if (currentSection) {
        currentSection.content = markdown.render(currentSection.content.trim());
        sections.push(currentSection);
      }
      currentSection = {
        title: markdown.render(line),
        content: '',
      };
    } else if (currentSection) {
      currentSection.content += line + '\n';
    }
  });

  if (currentSection) {
    currentSection.content = markdown.render(currentSection.content.trim());
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
    padding-left: 1.5rem
    margin: 0

    li
      padding: .25em 0
      margin: 0

/* Style du code Markdown */
.markdown-content
  :deep h1,
  :deep h2,
  :deep h3,
  :deep h4
    margin: 1.5em 0 .5em
  :deep(pre)
    padding: 1rem
    border-radius: 6px
    overflow-x: auto
    font-size: 0.875rem
    margin: .5rem 0
</style>
