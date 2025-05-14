<!-- u23655675 Arran Lamond -->

<template>
  <div class="post-container">
    <NuxtLink to="/" class="back-link">← Back to all posts</NuxtLink>
    
    <article class="post-content">
      <h1>{{ post.title }}</h1>
      <div class="post-meta">
        <span class="category" v-if="post.category">
          Category: {{ post.category.Category }}
        </span>
      </div>
      
      <div class="post-body">
        <!-- Render newlines as paragraphs -->
        <p v-for="(paragraph, index) in post.content.split('\n')" 
           :key="index"
           v-html="paragraph">
        </p>
      </div>
    </article>g
  </div>
</template>

<script setup>
const route = useRoute();
const { slug } = route.params;

// Fetch the specific post by slug
const { data: postData } = await useFetch(
  `http://localhost:1337/api/blog-posts?filters[slug][$eq]=${slug}`
);

// Extract the post from the response
const post = postData.value?.data?.[0] || null;

// Handle case where post doesn't exist
if (!post) {
  throw createError({ statusCode: 404, statusMessage: 'Post Not Found' });
}

</script>

<style scoped>
.post-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
}

.back-link {
  display: inline-block;
  margin-bottom: 2rem;
  color: #007bff;
  text-decoration: none;
}

.back-link:hover {
  text-decoration: underline;
}

.post-content {
  line-height: 1.6;
}

.post-content h1 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.post-meta {
  display: flex;
  gap: 1.5rem;
  margin-bottom: 2rem;
  color: #666;
  font-size: 0.9rem;
}

.post-body {
  margin-top: 2rem;
}

.post-body p {
  margin-bottom: 1.5rem;
}
</style>