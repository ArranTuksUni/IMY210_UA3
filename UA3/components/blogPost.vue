<!-- u23655675 Arran Lamond -->
<template>
  <div class="blog-post">
    <h1 class="title">{{ post.title }}</h1>
    
    <div class="meta">
      <span class="author">
        By {{ post.author.Name }} {{ post.author.Surname }}
      </span>
      <span class="category">
        Category: {{ post.category.Category }}
      </span>
    </div>
    
    <div class="content">
      {{ post.content }}
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  post: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
.blog-post {
  max-width: 800px;
  margin: 0 auto;
  padding: 1rem;
}

.title {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: #2c3e50;
}

.meta {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
  color: #666;
  font-size: 0.9rem;
  flex-wrap: wrap;
}

.category {
  color: #4299e1;
  font-weight: 500;
}

.content {
  line-height: 1.6;
  font-size: 1.1rem;
  white-space: pre-line;
}
</style>