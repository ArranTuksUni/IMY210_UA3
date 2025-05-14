<!-- u23655675 Arran Lamond -->
<template>
  <nav class="navbar">
    <NuxtLink to="/" class="nav-link">Home</NuxtLink>
    <NuxtLink to="/search" class="nav-link">Search</NuxtLink>
    <NuxtLink to="/blog" class="nav-link">Blog Page</NuxtLink>
  </nav>
</template>

<script setup>
// No script needed for basic navigation
</script>

<style scoped>
.navbar {
  background-color: #f8f9fa;
  padding: 1rem;
  margin-bottom: 2rem;
}

.nav-link {
  margin-right: 1rem;
  text-decoration: none;
  color: #333;
  font-weight: 500;
}

.nav-link:hover {
  color: #007bff;
}

.nav-link.router-link-active {
  color: #007bff;
  text-decoration: underline;
}
</style>