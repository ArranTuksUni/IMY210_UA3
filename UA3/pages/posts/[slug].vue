<template>
  <div class="page-wrapper">
    <NavBar />
    <div class="container">
      <div v-if="loading" class="loading">Loading...</div>
      
      <BlogPost 
        v-else-if="blogPost" 
        :post="formattedPost" 
      />
      
      <div v-else class="empty-state">
        <h1>Blog Page</h1>
        <p>No specific blog post chosen</p>
      </div>
      
      <NuxtLink to="/" class="back-button">
        ← Back to all posts
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const slug = route.params.slug;

const blogPost = ref(null);
const loading = ref(true);

const { data } = await useFetch(
  `http://localhost:1337/api/blog-posts?filters[slug][$eq]=${slug}&populate=category&populate=author`
);

const formattedPost = computed(() => {
  if (!blogPost.value) return null;
  
  const post = blogPost.value.attributes || blogPost.value;
  
  return {
    title: post.title,
    content: post.content,
    author: {
      Name: post.author.Name,
      Surname: post.author.Surname
    },
    category: {
      Category: post.category.Category
    }
  };
});

if (data.value?.data?.length > 0) {
  blogPost.value = data.value.data[0];
}

loading.value = false;
</script>
<style >
/* Global light blue background for entire HTML */
html, body {
  background-color: lightblue; /* Soft light blue */
  margin: 0;
  padding: 0;
  min-height: 100vh;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>

<style scoped>
.page-wrapper {
  background-color: lightblue; /* Light blue background */
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 2rem;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.loading {
  text-align: center;
  padding: 2rem;
  color: #2c3e50;
}

.empty-state {
  text-align: center;
  padding: 4rem 0;
}

.empty-state h1 {
  margin-bottom: 1rem;
  color: #2c3e50;
}

.empty-state p {
  color: #666;
  font-size: 1.1rem;
}

.back-button {
  display: inline-block;
  margin-top: 2rem;
  padding: 0.75rem 1.5rem;
  background-color: #90EE90; /* Light green */
  color: #2c3e50; /* Dark text */
  text-decoration: none;
  border-radius: 6px;
  font-weight: 500;
  transition: all 0.2s ease;
  border: none;
  cursor: pointer;
  font-size: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.back-button:hover {
  background-color: #76D7C4; /* Slightly darker green */
  transform: translateY(-1px);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.back-button:active {
  transform: translateY(0);
}
</style>