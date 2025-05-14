<!-- u23655675 Arran Lamond -->
<template>
  <div>
    <NavBar />
    <div class="container">
      <h1>Search Blog Posts</h1>
      
      <SearchBar @search="handleSearch" />
      
      <BlogList 
        :blogs="filteredBlogs"
        v-if="filteredBlogs.length > 0"
      />
      
      <p v-else-if="searchQuery" class="no-results">
        No results found for "{{ searchQuery }}"
      </p>
      
      <p v-else class="start-searching">
        
      </p>
    </div>
  </div>
</template>

<script setup>
const { data: blogs } = await useFetch('http://localhost:1337/api/blog-posts?populate=author');

const searchQuery = ref('');
const filteredBlogs = ref([]);

const handleSearch = (query) => {
  searchQuery.value = query.toLowerCase().trim();
  
  if (!searchQuery.value) {
    filteredBlogs.value = [];
    return;
  }

  filteredBlogs.value = blogs.value.data.filter(blog => {
    const titleMatch = blog.title.toLowerCase().includes(searchQuery.value);
    const authorMatch = `${blog.author.Name} ${blog.author.Surname}`.toLowerCase().includes(searchQuery.value);
    return titleMatch || authorMatch;
  });
};
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 1rem;
}

h1 {
  margin-bottom: 2rem;
  color: #2c3e50;
}

.no-results,
.start-searching {
  text-align: center;
  margin-top: 2rem;
  color: #666;
}
</style>