<!-- u23655675 Arran Lamond -->
<template>
  <div class="category-filter">
    <label for="category">Filter by Category:</label>
    <select 
      id="category" 
      v-model="selectedCategory"
      @change="emitFilter"
      class="filter-select"
    >
      <option value="">All Categories</option>
      <option 
        v-for="category in uniqueCategories" 
        :key="category" 
        :value="category"
      >
        {{ category }}
      </option>
    </select>
  </div>
</template>

<script setup>
const props = defineProps({
  blogPosts: {
    type: Array,
    required: true
  }
});

const selectedCategory = ref('');

const emit = defineEmits(['filter']);

const emitFilter = () => {
  emit('filter', selectedCategory.value);
};

// Extract unique category names from blog posts
const uniqueCategories = computed(() => {
  const categories = new Set();
  
  props.blogPosts.forEach(post => {
    if (post.category?.Category) {
      categories.add(post.category.Category);
    }
  });
  
  return Array.from(categories).sort();
});
</script>

<style scoped>
.category-filter {
  margin-bottom: 2rem;
}

.filter-select {
  margin-left: 0.5rem;
  padding: 0.5rem;
  border-radius: 4px;
  border: 1px solid #ddd;
}
</style>