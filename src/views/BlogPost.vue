<template>
  <div class="blog-post-page">
    <h1>{{ post.title }}</h1>
    <p>{{ post.timestamp }}</p>
    <div v-html="post.content"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const post = ref({ title: '', content: '', timestamp: '' });

const loadPost = async () => {
  const files = import.meta.glob('../articles/*.md', { as: 'raw' });
    const file = Object.keys(files)[route.params.id - 1];
    const content = await files[file](); // Markdown content as string
    const lines = content.split('\n');

  post.value = {
    title: lines[0]?.replace('# ', '') || 'Untitled',
    timestamp: lines[1]?.replace('Timestamp: ', '') || 'No timestamp available',
    content: lines.slice(2).join('\n')
  };
};

onMounted(() => {
  loadPost();
});
</script>

<style scoped>
.blog-post-page {
  padding: 20px;
  color: var(--text-color, #000); /* Default color */
}

.dark .blog-post-page {
  color: #d1d5db; /* Light gray color for dark mode */
}
</style>
