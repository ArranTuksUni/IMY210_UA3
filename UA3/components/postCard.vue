<!-- u23655675 Arran Lamond -->
<template>
  <div class="blog-card">
    <!-- Blog Title (bold) -->
    <h2 class="blog-title">{{ blog.title }}</h2>
    
    <!-- Author Name -->
    <p class="blog-author">
      By {{ getAuthorName() }}
    </p>
    
    <!-- Content Preview (50 characters) -->
    <p class="blog-preview">{{ contentPreview }}</p>
    
    <!-- Read More Button -->
    <NuxtLink 
      :to="`/blog-post/${blog.slug}`"
      class="read-more-button"
    >
      Read More
    </NuxtLink>
  </div>
</template>

<script setup>
const props = defineProps({
  blog: {
    type: Object,
    required: true
  }
});

// Get 50 character preview of content
const contentPreview = computed(() => {
  const content = props.blog.content || '';
  return content.length > 75 
    ? `${content.substring(0, 75)}...` 
    : content;
});

// Helper function to get author's full name
const getAuthorName = () => {
  const author = props.blog?.author;

  if (author?.Name && author?.Surname) {
    return `${author.Name} ${author.Surname}`;
  }

  return 'Unknown Author';

};
</script>

<style scoped>
.blog-card {
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  background-color: white;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.blog-title {
  font-weight: bold;
  font-size: 1.25rem;
  margin: 0 0 0.5rem 0;
  color: #1a202c;
}

.blog-author {
  color: #4a5568;
  font-size: 0.875rem;
  margin: 0 0 0.75rem 0;
}

.blog-preview {
  color: #2d3748;
  margin: 0 0 1rem 0;
  line-height: 1.5;
}

.read-more-button {
  display: inline-block;
  background-color: #4299e1;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  text-decoration: none;
  font-size: 0.875rem;
  transition: background-color 0.2s;
}

.read-more-button:hover {
  background-color: #3182ce;
}
</style>