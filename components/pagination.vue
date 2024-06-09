<template>
    <div class="flex justify-between items-center mt-4 mb-4">
      <p class="text-gray-700">Showing {{ filteredCharacters.length }} of {{ characters.length }} characters (Total: {{ totalCount }})</p>
      <div class="flex space-x-4">
        <button @click="fetchPage" :disabled="loading || !nextPageUrl" class="bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-700 disabled:opacity-50">
          Load More
        </button>
        <button @click="fetchAllPages" :disabled="loading || !nextPageUrl" class="bg-green-500 text-white py-2 px-4 rounded hover:bg-green-700 disabled:opacity-50">
          Load All
        </button>
      </div>
    </div>
</template>
  
<script setup>
  defineProps({
    filteredCharacters: Array,
    characters: Array,
    totalCount: Number,
    loading: Boolean,
    nextPageUrl: String,
    fetchPage: Function,
    fetchAllPages: Function
  });
</script>
  