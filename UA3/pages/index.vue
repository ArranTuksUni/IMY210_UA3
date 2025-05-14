<!-- u23655675 Arran Lamond -->
<template>
  <div>
    <NavBar />
    <div class="container">
      <h1>Welcome to the Blog</h1>
      
      <CategoryDropdown
        :blog-posts="blogs.data"
        @filter="handleFilter"
      />
      
      <BlogList 
        :blogs="filteredBlogs"
      />
    </div>
  </div>
</template>

<script setup>
const { data: blogs } = await useFetch('http://localhost:1337/api/blog-posts?populate=category&&populate=author');

const selectedCategory = ref('');

const handleFilter = (categoryName) => {
  selectedCategory.value = categoryName;
};

const filteredBlogs = computed(() => {
  if (!selectedCategory.value) return blogs.value.data;
  
  return blogs.value.data.filter(blog => {
    // Direct access to category name without .attributes or .data
    const blogCategory = blog.category?.Category || 
                        blog.attributes?.category?.data?.attributes?.Category ||
                        blog.attributes?.category?.attributes?.Category;
    return blogCategory === selectedCategory.value;
  });
});
</script>

<style>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 1rem;
}

h1 {
  margin-bottom: 2rem;
  color: #2c3e50;
}
</style>