<!-- u23655675 Arran Lamond -->
<template>
  <div class="search-bar">
    <input
      type="text"
      v-model="query"
      @input="handleInput"
      placeholder="Search by title or author..."
      class="search-input"
    />
  </div>
</template>

<script setup>
const query = ref('');
const emit = defineEmits(['search']);

const handleInput = () => {
  emit('search', query.value);
};
</script>

<style scoped>
.search-bar {
  margin-bottom: 2rem;
}

.search-input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}
</style>