<template>
  <div v-html="markdown.render(contenuMarkdown)" class="markdown-content" />
</template>

<script setup>
import hljs from 'highlight.js';
import 'highlight.js/styles/atom-one-dark.css'; // Tu peux changer le thème si tu veux
import MarkdownIt from 'markdown-it';
import {onMounted, ref} from "vue";

// Définition des props
const props = defineProps({
  source: {
    type: String,
    required: true,
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


</script>
