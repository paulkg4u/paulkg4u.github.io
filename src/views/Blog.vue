<template>
    <div class="blog-page">
      <!-- <h1>Blog Page</h1> -->
      <div class="blog-list">
        <!-- Loop through posts and display title and excerpt -->
        <div class="blog-post" v-for="post in posts" :key="post.id">
          <h2>{{ post.title }}</h2>
          <p>{{ post.excerpt }}</p>
          <router-link :to="'/blog/' + post.id">Read more</router-link>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  // Reactive variable to store posts
  const posts = ref([]);
  
  // Function to load posts from markdown files
  const loadPosts = async () => {
    // Import all markdown files from the articles directory
    const files = import.meta.glob('../articles/*.md', { as: 'raw' });

        posts.value = await Promise.all(
        Object.keys(files).map(async (file, index) => {
            const content = await files[file](); // Markdown content as string
            const lines = content.split('\n');
            const title = lines[0]?.replace('# ', '') || 'Untitled';
            const excerpt = lines.slice(1, 3).join(' ') || 'No excerpt available';

            return { id: index + 1, title, excerpt };
        })
        );
  };
  
  // Load posts when the component is mounted
  onMounted(() => {
    loadPosts();
  });
  </script>
  
  <style scoped>
  .blog-page {
    padding: 20px;
    color: var(--text-color, #000); /* Default color */
  }
  
  .blog-list {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
  
  .blog-post {
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
  }

  .dark .blog-page {
  color: #d1d5db; /* Light gray color for dark mode */
}
  </style>