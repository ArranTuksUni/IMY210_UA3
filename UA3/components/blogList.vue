<!-- u23655675 Arran Lamond -->
<template>
  <div class="blog-list">
    <PostCard 
      v-for="blog in filteredBlogs" 
      :key="blog.id" 
      :blog="blog" 
    />
  </div>
</template>

<script setup>
const props = defineProps({
  blogs: {
    type: Array,
    required: true
  },
  selectedCategory: {
    type: String,
    default: ''
  }
});

const filteredBlogs = computed(() => {
  if (!props.selectedCategory) return props.blogs;
  return props.blogs.filter(blog => 
    blog.attributes.category.data.id.toString() === props.selectedCategory
  );
});
</script>

<style scoped>
.blog-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}
</style>